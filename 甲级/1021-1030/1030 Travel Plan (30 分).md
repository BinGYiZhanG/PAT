### 标准```Dijsktra+DFS```

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <vector>
using namespace std;

const int inf=0x3f3f3f3f;
int e[510][510],cost[510][510];
int dis[510],c[510];
bool vis[510];
vector<int> pre[510];

int n,m,st,ed;

void Dijsktra(){
    dis[st]=0;
    c[st]=0;
    for(int i=0;i<n;i++){
        int u=-1,minn=inf;
        for(int j=0;j<n;j++){
            if(dis[j]<minn&&vis[j]==false){
                u=j;
                minn=dis[j];
            }
        }
        if(u==-1)
            break;
        vis[u]=true;
        for(int v=0;v<n;v++){
            if(vis[v]==false&&e[u][v]!=inf){
                if(dis[v]>dis[u]+e[u][v]){
                    dis[v]=dis[u]+e[u][v];
                    c[v]=c[u]+cost[u][v];
                    pre[v].clear();
                    pre[v].push_back(u);
                }
                else if(dis[v]==dis[u]+e[u][v]){
                    if(c[v]>c[u]+cost[u][v]){
                        c[v]=c[u]+cost[u][v];
                        pre[v].push_back(u);
                    }
                }
            }
        }
    }
}


vector<int> tempath,ans;
int mincost=inf;
void DFS(int v){
    tempath.push_back(v);
    if(v==st){
        int tempcost=0;
        for(int i=tempath.size()-1;i>0;i--){
            int id=tempath[i],nextid=tempath[i-1];
            tempcost+=cost[id][nextid];
        }
        if(mincost>tempcost){
            mincost=tempcost;
            ans=tempath;
        }
        tempath.pop_back();
        return ;
    }
    for(int i=0;i<(int)pre[v].size();i++){
        DFS(pre[v][i]);
    }
    tempath.pop_back();
    return ;
}


int main()
{
    int a,b;
    scanf("%d%d%d%d",&n,&m,&st,&ed);
    memset(e,inf,sizeof(e));
    memset(cost,inf,sizeof(cost));
    memset(dis,inf,sizeof(dis));
    memset(c,inf,sizeof(c));
    memset(vis,false,sizeof(vis));
    for(int i=0;i<m;i++){
        scanf("%d%d",&a,&b);
        scanf("%d%d",&e[a][b],&cost[a][b]);
        e[b][a]=e[a][b];
        cost[b][a]=cost[a][b];
    }

    Dijsktra();
    DFS(ed);

    for(int i=ans.size()-1;i>=0;i--){
        printf("%d ",ans[i]);
    }
    printf("%d %d\n",dis[ed],mincost);
    return 0;
}


```
