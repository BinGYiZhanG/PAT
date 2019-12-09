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


* 注意：总是想着在BFS的while循环内依靠一个layers来记录层数，这明显是不可能的，因为一层可能有多个节点，不可能只通过一个layers来记录

```c++
#include <bits/stdc++.h>

using namespace std;

const int maxn=100+10;
int n,m;
vector<int> G[maxn];
int layer[maxn];///每层有多少个叶结点

void BFS(){
    queue<int> q;
    q.push(1);
    int layers=2///控制层数
    while(!q.empty()){
        int top=q.front();
        q.pop();
        for(int i=0;i<G[top].size();i++){
            int tmp=G[top][i];
            if(G[tmp].size()==0){
                layer[layers]++;
            }
            q.push(tmp);
        }
        
    }
}

int main(){
    scanf("%d%d",&n,&m);
    for(int i=0;i<m;i++){
        int parent,k,child;
        scanf("%d%d",&parent,&k);
        for(int j=0;j<k;j++){
            scanf("%d",&child);
            G[parent].push_back(child);
        }
    }
    ///如何找到根节点?根节点为01
    
}
```
