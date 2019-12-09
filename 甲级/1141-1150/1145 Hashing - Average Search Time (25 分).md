### 输入
* 第一行，MSize，用户定义的表大小；N，输入的数字的个数；M，被发现的键值个数，所有元素都不超过```10^{4}```
* 第二行，n个整数，
* 第三行，m个整数
所有数字都不超过$10_{5}$

### 输出
如果插入一些数字是不可能的，则打印```X cannot be inserted```,```X```是输入数字<br>
最后打印查找M个键值的平均查找时间，精确到小数点后1位<br>

* 注意：
  * 线性探测平方时间的范围是:```0~Msize-1```
  * 最后，计算平均查找时间时，线性探测时，范围是```0~Msize```

```
#include <iostream>
#include <vector>

using namespace std;

bool isprime(int n) {
	for (int i = 2; i*i <= n; i++) {
		if (n%i == 0)
			return false;
	}
	return true;
}

int main() {
	int n, m, msize, a;
	scanf("%d%d%d", &msize, &n, &m);
	while (!isprime(msize))
		msize++;
	vector<int> v(msize);
	for (int i = 0; i < n; i++) {
		scanf("%d", &a);
		int flag = 0;
		for (int j = 0; j < msize; j++) {//循环范围
			int pos = (a + j * j) % msize;
			if (v[pos] == 0) {
				v[pos] = a;
				flag = 1;
				break;
			}
		}
		if (!flag)
			printf("%d cannot be inserted.\n", a);
	}
	int ans = 0;
	for (int i = 0; i < m; i++) {
		scanf("%d", &a);
		for (int j = 0; j <= msize; j++) {//是"=",
			ans++;
			int pos = (a + j * j) % msize;
			if (v[pos] == a || v[pos] == 0)//如果有插入位置元素是0,
				break;//如果插入的就是该元素，或者插入的位置为0，则结束循环，
		}
	}
	printf("%.1lf\n", ans*1.0 / m);
	return 0;
}
```


