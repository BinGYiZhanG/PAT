
```cpp
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>
using namespace std;

const int maxn = 100010;
const int mod = 1000000007;
int main() {
	string str;
	int numleftP[maxn] = {0};
	cin >> str;
	int len = str.length();
	for (int i = 0; i < len; i++) {
		if (i > 0)//顺序不能颠倒
			numleftP[i] = numleftP[i - 1];
		if (str[i] == 'P')
			numleftP[i]++;
	}
	int numrighT = 0, ans = 0;
	for (int i = len - 1; i >= 0;i--) {
		if (str[i] == 'T')
			numrighT++;
		else if (str[i] == 'A')
			ans = (ans + numrighT * numleftP[i]) % mod;
	}
	printf("%d", ans);
	return 0;
}
```
