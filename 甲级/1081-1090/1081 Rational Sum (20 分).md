### 题意
* 假定N个分数以```numerator/denominator```，你应该计算它们的和。<br>
### 输入：<br>
* 每一个输入包含一个测试用例。N个分数```a1/b1 a2/b2 ...```，所有分子分母都是长整型范围内，如果有一个负数，符号应该在分子之前。<br>
### 输出：<br>
* 输出最简单的形式```integer numerator/denominator ```<br>
* 输出```integer```是和的整数部分，如果```numerator < denominator ```，并且分子和分母之间没有最小公倍数，你应该输出它们的分数部分。如果整数部分```(integer)```为0的话。<br>
```cpp
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <cmath>
using namespace std;
typedef long long ll;
ll gcd(ll a, ll b) {
	ll temp = a;
	while (a%b != 0) {
		a = b;
		b = temp % b;
		temp = a;
	}
	return b;
}

struct Fraction {
	ll up, down;
};

Fraction reduction(Fraction result) {
	if (result.down < 0) {
		result.up = -result.up;
		result.down = -result.down;
	}
	if (result.up == 0) {
		result.down = 1;
	}
	else {
		int d = gcd(abs(result.up), abs(result.down));
		result.up /= d;
		result.down /= d;
	}
	return result;
}

Fraction add(Fraction f1, Fraction f2) {
	Fraction result;
	result.up = f1.up*f2.down + f2.up*f1.down;
	result.down = f1.down*f2.down;
	return reduction(result);
}

void showResult(Fraction r) {
	reduction(r);
	if (r.down == 1)
		printf("%lld\n", r.up);
	else if (abs(r.up) > r.down) {
		printf("%lld %lld/%lld\n", r.up / r.down, abs(r.up) % r.down, r.down);
	}
	else {
		printf("%lld/%lld\n", r.up, r.down);
	}
}

int main() {
	int n;
	scanf("%d", &n);
	Fraction sum, tmp;
	sum.up = 0;
	sum.down = 1;
	for (int i = 0; i < n; i++) {
		scanf("%lld/%lld", &tmp.up, &tmp.down);
		sum = add(sum, tmp);
	}
	showResult(sum);
	return 0;
}

```
