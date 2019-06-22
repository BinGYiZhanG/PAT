#### 思路：
### 设置该城市已访问，然后，寻找连通块，即要修复的公路数

```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxn=1010;
int n,m,k;///城市数，高速公路数，需要被检查的城市数量
bool vis[maxn];
int e[maxn][maxn];

void dfs(int v){
    vis[v]=true;
    for(int i=1;i<=n;i++){
        if(vis[i]==false && e[v][i]==1){
            dfs(i);
        }
    }
}

int main(){
    scanf("%d%d%d",&n,&m,&k);
    fill(e[0],e[0]+maxn*maxn,0);
    for(int i=0;i<m;i++){
        int c1,c2;
        scanf("%d%d",&c1,&c2);
        e[c1][c2]=e[c2][c1]=1;
    }

    for(int i=0;i<k;i++){
        int cnt=0;
        fill(vis,vis+maxn,0);
        int city;
        scanf("%d",&city);
        vis[city]=true;
        for(int j=1;j<=n;j++){
            if(vis[j]==false){
                dfs(j);
                cnt++;
            }
        }
        printf("%d\n",cnt-1);
    }
    return 0;
}
```
