
题意：查询在数组满足条件 ```大于左边的元素，小于右边的元素``` 的元素数

* 遍历n个数，判断每个数左右两边的数是否符合，此数左边的数都小于此数，此数右边的数都大于此数

* 注意格式输出，当不存在时，该如何输出
```
if(cnt==0){
        printf("\n");///注意格式输出
    }
```

本人代码没A，超时了
复杂度也就是O(n^2)，但是就是超时
### 另外还得注意输出格式,cnt=0的情况
![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07120222.png)


```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;

const int maxn=100010;
int a[maxn],b[maxn];

int main()
{
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d",a+i);
    }
    int cnt=0;
    for(int i=0;i<n;i++){
        int lf=i-1,rt=i+1;
        bool lflag=true,rflag=true;
        while(lf>=0){
            if(a[lf]>a[i]){
                lflag=false;
                break;
            }
            lf--;
        }
        if(lflag==false){
            continue;
        }

        while(rt<n){
            if(a[rt]<a[i]){
                rflag=false;
                break;
            }
            rt++;
        }
        if(rflag==false){
            continue;
        }
        b[cnt++]=a[i];
    }
    if(cnt==0){
        printf("-1\n");
    }
    else{
        sort(b,b+cnt);
        printf("%d\n",cnt);
        for(int i=0;i<cnt;i++){
            if(i==0)
                printf("%d",b[i]);
            else
                printf(" %d",b[i]);
        }
    }
    return 0;
}

```

《算法笔记》A的代码
## 思想：空间换时间，加存储最大/最小 值的数组
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
using namespace std;

const int maxn = 100010;
int a[maxn];
int leftmax[maxn], rightmin[maxn];
int ans[maxn], num = 0;
int main() {
	int n,cnt = 0;//cnt记录主元个数
	cin >> n;
	for (int i = 0; i < n; i++) {
		cin >> a[i];
	}
	//我能想到的是，二重循环比较大小,
	//算法笔记，leftnum[i]记录第i位之前最大的元素,
	fill(leftmax, leftmax + maxn, 0);
	fill(rightmin, rightmin + maxn, 0);

	//leftmax[0] = a[0];
	leftmax[0] = 0;
	for (int i = 1; i < n; i++) {
		//leftmax[i] = max(leftmax[i - 1], a[i]);
		leftmax[i] = max(leftmax[i - 1], a[i-1]);
	}

	//rightmin[n - 1] = a[n - 1];
	rightmin[n - 1] = 0x3fffffff;
	for (int i = n - 2; i >= 0; i--) {
		//rightmin[i] = min(rightmin[i + 1], a[i]);
		rightmin[i] = min(rightmin[i + 1], a[i+1]);
	}

	for (int i = 0; i < n; i++) {
		if (leftmax[i]<a[i] && rightmin[i]>a[i]) {
			ans[num++] = a[i];
		}
	}
	printf("%d\n", num);
	if (num == 0) {//注意num==0的情况输出
		printf("\n");
	}
	else {
		for (int i = 0; i < num; i++) {
			if (i != 0) {
				printf(" ");
			}
			printf("%d", ans[i]);
		}
	}
	return 0;
}
```







