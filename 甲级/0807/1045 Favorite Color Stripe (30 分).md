
#### 我写的代码存在一个问题就是没有把，不喜欢的颜色剔除
```cpp
#include <cstdio>
#include <iostream>
#include <cstring>

using namespace std;

int book[210];
int input[10010];
int dp[210];


int main(){
    int n;
    scanf("%d",&n);
    int m;
    scanf("%d",&m);
    for(int i=1;i<=m;i++){
        int tmp;
        scanf("%d",&tmp);
        book[tmp]=i;
    }
    int l;
    scanf("%d",&l);
    for(int i=0;i<l;i++){
        scanf("%d",&input[i]);
    }

    memset(input,0,sizeof(input));

    int ans=0;
    for(int i=1;i<l;i++){
        for(int j=0;j<i;j++){
            if(book[input[i]]>=book[input[j]]&&dp[i]<dp[j]+1)
                dp[i]=dp[j]+1;
            ans=max(ans,dp[i]);
        }
    }
    printf("%d\n",ans);
    return 0;
}

```


#### 剔除不喜欢的，然后就是求最长递增序列

```cpp
#include <cstdio>
#include <iostream>
#include <cstring>

using namespace std;

int book[210];
int input[10010];
int dp[210];
int num=0;

int main(){
    int n;
    scanf("%d",&n);
    int m;
    scanf("%d",&m);
    for(int i=1;i<=m;i++){
        int tmp;
        scanf("%d",&tmp);
        book[tmp]=i;
    }
    int l;
    scanf("%d",&l);
    int x;
    for(int i=0;i<l;i++){
        scanf("%d",&x);
        if(book[x]>=1)
            input[num++]=book[x];
    }

   // memset(dp,1,sizeof(dp));加了这句出现错误

    int ans=0;
    for(int i=0;i<num;i++){
        dp[i]=1;
        for(int j=0;j<i;j++){
            if(input[i]>=input[j]&&dp[i]<dp[j]+1)
                dp[i]=dp[j]+1;
        }
        ans=max(ans,dp[i]);
    }
    printf("%d\n",ans);
    return 0;
}

```


另一种做法
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>

using namespace std;
const int maxc = 210;
const int maxn = 10010;
int like[maxc] = { 0 };
int given[maxn] = { 0 };
int len[maxc][maxn] = { 0 };

int LCS(int row, int col) {
//	int max;
	for (int i = 1; i <= row; i++) {
		for (int j = 1; j <= col; j++) {
			/*//不允许重复的情况
			if (like[i] == given[j]) {
				len[i][j] = len[i - 1][j - 1] + 1;
			}
			else {
				len[i][j] = max(len[i - 1][j], len[i][j - 1]);
			}*/
			//允许重复的情况
			/*max = len[i - 1][j - 1];
			if (max < len[i - 1][j])	max = len[i - 1][j];
			if (max < len[i][j - 1])	max = len[i][j - 1];
			if (like[i] == given[j])
				len[i][j] = max + 1;
			else
				len[i][j] = max;*/
			if (like[i] == given[j])
				len[i][j] = max(len[i][j - 1], len[i - 1][j]) + 1;
			else
				len[i][j] = max(len[i][j - 1], len[i - 1][j]);
		}
	}
	return len[row][col];
}

int main() {
	int n, m, l;
	cin >> n >> m;
	for (int i = 0; i < m; i++) {
		cin >> like[i+1];//**从第一位开始记录**
	}
	cin >> l;
	for (int i = 0; i < l; i++) {
		cin >> given[i+1];
	}
	int res = LCS(m, l);
	printf("%d", res);
	return 0;
}
```


