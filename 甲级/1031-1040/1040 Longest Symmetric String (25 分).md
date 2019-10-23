### 错误点：
* 忘了递归进行了```dp[i+1][j-1]==1 ```

![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/08071308.png)

```cpp
#include <iostream>
#include <cstdio>
#include <string>

using namespace std;

int dp[1010][1010];
string line;

int main()
{
    getline(cin,line);
    //cout<<line<<endl;
    int ans=1;///记录最大长度
    for(int i=1;i<(int)line.size();i++){
        dp[i][i]=1;
        if(line[i]==line[i-1]){
            dp[i-1][i]=1;
            ans=2;
        }
    }

    for(int L=3;L<=(int)line.size();L++){
        for(int i=0;i+L-1<(int)line.size();i++){
            int j=i+L-1;
            if(line[i]==line[j]){
                dp[i][j]=1;
                ans=L;
            }
        }
    }
    printf("%d\n",ans);
    return 0;
}
```

满分代码:
```cpp
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>

using namespace std;
//const int maxn = 10010;
//int dp[maxn][maxn];
const int maxn = 10010;
bool dp[maxn][maxn];
int main() {
	string s;
	getline(cin, s);
	int len = s.length();
	fill(dp[0], dp[0] + maxn * maxn, false);

	int ans = 1;
	for (int i = 0; i < len; i++) {
		for (int j = 0; j <= i; j++) {
			if (i - j < 2)
				dp[i][j] = s[i] == s[j];
			else
				dp[i][j] = s[i] == s[j] && dp[i + 1][j - 1];
			if (dp[i][j])
				ans = max(j - i + 1, ans);
		}
	}
	printf("%d", ans);
	//int len = s.length(), ans = 1;
	//for (int i = 0; i < len; i++) {
	//	dp[i][i] = 1;
	//	if (i < len - 1) {
	//		if (s[i] == s[i + 1]) {
	//			dp[i][i + 1] = 1;
	//			ans = 2;
	//		}
	//	}
	//}
	//for (int L = 3; L <= len; L++) {
	//	for (int i = 0; i + L - 1 < len; i++) {
	//		//为什么是i+L-1，而不是i+L，
	//		//举例len=3时,初始:i+L-1=2（终点）,而非i+L=3
	//		int j = i + L - 1;
	//		if (s[i] == s[j] && dp[i + 1][j - 1] == 1) {
	//			dp[i][j] = 1;
	//			ans = L;
	//		}
	//	}
	//}
	printf("%d\n", ans);
	return 0;
}
```
