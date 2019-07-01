
### 二分:查找第一个大于X的元素，
### 思想:
  * 如果j是查找的下标，
    * 如果sum[j-1]-sum[i-1]==S，说明第j-1个元素就是符合题意的元素
    * 否则sum[j]-sum[i-1]，是最接近S的数值
  * 关于求和sum数组相减，得到的数组之和范围，见下图
  ![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07012030.png)

```cpp
#include <iostream>
#include <algorithm>
#include <queue>

using namespace std;
const int maxn = 100010;
int sum[maxn], n, S, nearS = 100000010;

int upper_bound(int L, int R, int X) {
	int left = L, right = R, mid;
	while (left < right) {
		mid = (left + right) / 2;
		if (sum[mid] > X)
			right = mid;
		else
			left = mid + 1;
	}
	return left;
}

int main() {
	scanf("%d%d", &n, &S);
	sum[0] = 0;
	for (int i = 1; i <= n; i++) {
		scanf("%d", &sum[i]);
		sum[i] += sum[i - 1];
	}
	for (int i = 1; i <= n; i++) {
		//sum[j]-sum[i-1]:计算A[i]~A[j]的和
		//n+1对应着，从0~n的n,即上界
		int j = upper_bound(i, n + 1, sum[i - 1]+ S);
		if (sum[j - 1] - sum[i - 1] == S) {
			nearS = S;
			break;
		}
		else if (j <= n && sum[j] - sum[i - 1] < nearS) {
			nearS = sum[j] - sum[i - 1];
		}
	}
	for (int i = 1; i <= n; i++) {
		int j = upper_bound(i, n + 1, sum[i - 1] + nearS);
		if (sum[j - 1] - sum[i - 1] == nearS) {
			printf("%d-%d\n", i, j - 1);
		}
	}
	return 0;
}
```
