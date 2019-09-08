### 题目大意：
* 求最大连续子序列和，输出最大的和以及这个子序列的开始值和结束值。如果所有数都小于0，
* 那么认为最大的和为0，并且输出首尾元素～

#### 21分代码

* ```if(dp[i]<dp[i-1]+A[i]) ```,错
* ```if(A[i]<dp[i-1]+A[i]) ```,对
* 第二种情况才是符合赋值条件的，因为，在条件下，
 * 不满足条件，```dp[i]=A[i]```
 * 满足条件，```dp[i]=dp[i-1]+A[i]```
 * ```dp[i]```是结果，而```A[i]```是过程，不能用结果```dp[i]```进行判断```if(dp[i]<dp[i-1]+A[i]) ```赋值,再给结果```dp[i]```
 
 
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <string>
#include <algorithm>
#include <cmath>
using namespace std;

int a[10010], dp[10010], A[10010];

int main() {
	int K;
	bool flag=false;
	scanf("%d",&K);
	for(int i=0;i<K;i++){
        scanf("%d",A+i);
        //if(A[i]>0)
        if(A[i]>=0)//=，测试点5
            flag=true;
	}

	if(!flag)
        printf("0 %d %d\n",A[0],A[K-1]);
    else{
    //    memset(dp,0,sizeof(dp));
    //    memset(a,0,sizeof(a));
        a[0]=0;
        dp[0]=A[0];
        for(int i=1;i<K;i++){
            if(dp[i]<dp[i-1]+A[i]){ 
                dp[i]=dp[i-1]+A[i];
                a[i]=a[i-1];
            }
            else
            {
                dp[i]=A[i];
                a[i]=i;
            }
        }
        int k=0;
        for(int i=1;i<K;i++){
            if(dp[i]>dp[k])
                k=i;
        }
        printf("%d %d %d\n",dp[k],A[a[k]],A[k]);
    }
}

```


```c++
#include <iostream>
#include <cstdio>
#include <algorithm>

using namespace std;
const int maxn=10000+10;

int A[maxn],dp[maxn];
///A[i]存放序列，dp[i]存放以A[i]结尾的连续序列的最大和
int n;
int st[maxn];///记录最大和的开头的序号

int main(){
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d",&A[i]);
    }
    dp[0]=A[0];
    st[0]=0;
    for(int i=1;i<n;i++){
        if(A[i]>dp[i-1]+A[i]){
            dp[i]=A[i];
            st[i]=i;
        }
        else{
            dp[i]=dp[i-1]+A[i];
            st[i]=st[i-1];
        }
        //dp[i]=max(A[i],dp[i-1]+A[i]);
    }
    int k=0;
    for(int i=1;i<n;i++){
        if(dp[i]>dp[k]){
            k=i;
        }
    }
    if(dp[k]>=0){
        //输出值最大的序列的数字，而非序号
        printf("%d %d %d\n",dp[k],A[st[k]],A[k]);
    }
    else{
        printf("0 %d %d\n",A[0],A[n-1]);
    }
    return 0;
}
```



```cpp
/*
#include <iostream>
#include <cstdio>
using namespace std;

const int maxn = 10010;
int s[maxn], dp[maxn], a[maxn];
int main() {
	int n;
	bool flag = false;
	cin >> n;
	for (int i = 0; i < n; i++) {
		cin >> s[i];
		if (s[i] >= 0)
			flag = true;
	}
	if (!flag) {
		printf("0 %d %d", s[0], s[n - 1]);
		return 0;
	}
	dp[0] = s[0];
	a[0] = 0;
	for (int i = 1; i < n; i++) {
		if (dp[i - 1] + s[i] < s[i]) {
			dp[i] = s[i];
			a[i] = i;
		}
		else {
			dp[i] = dp[i - 1] + s[i];
			a[i] = a[i - 1];
		}
	}
	int k = 0;
	for (int i = 1; i < n; i++) {
		if (dp[i] > dp[k])
			k = i;
	}

	//输出值最大的序列的数字，而非序号
	cout << dp[k] << " " << s[a[k]] << " " << s[k];
	return 0;
}
*/
```
