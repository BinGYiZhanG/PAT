### 题目大意：
* 给出一棵树，问每一层各有多少个叶子结点～

#### 思路：
* ```h[]```，记录结点的层数
* ```leaf[]```，记录每层的叶子节点个数


```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <queue>
#include <algorithm>
#include <vector>
using namespace std;

int n,m;
vector<int> G[110];
int leaf[110],h[110],maxh;

void BFS(){
    queue<int> q;
    q.push(1);

    while(!q.empty()){
        int tp=q.front();
        q.pop();

        if(G[tp].size()==0)
            leaf[h[tp]]++;///该层叶子数加1
        maxh=max(maxh,h[tp]);
        for(int i=0;i<G[tp].size();i++){
            int ch=G[tp][i];
            h[ch]=h[tp]+1;
            q.push(ch);
        }
    }
}

int main(){
    int p,k,ch;
    scanf("%d%d",&n,&m);
    for(int i=0;i<m;i++){
        scanf("%d%d",&p,&k);
        for(int j=0;j<k;j++){
            scanf("%d",&ch);
            G[p].push_back(ch);
        }
    }

    h[1]=1;
    BFS();
    for(int i=1;i<=maxh;i++){
        if(i==1)
            printf("%d",leaf[i]);
        else
            printf(" %d",leaf[i]);
    }

    return 0;
}

```
