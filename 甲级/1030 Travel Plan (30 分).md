只是再抄写一下《算法笔记》而已。。

### 1,Dijkstra+DFS
```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxv=510;
const int inf=0x3f3f3f3f;

int n,m,st,ed,G[maxv][maxv],cost[maxv][maxv];
int d[maxv],minCost=inf;
bool vis[maxv]={false};

vector<int> pre[maxv];
vector<int> tempPath,path;

void Dijkstra(int s){
    fill(d,d+maxv,inf);
    d[s]=0;
    for(int i=0;i<n;i++){
        int min_=inf,u=-1;
        for(int j=0;j<n;j++){
            if(vis[u]==false || d[j]<min_){
                min_=d[j];
                u=j;
            }
        }
        if(u==-1)
            return ;
        vis[u]=true;
        for(int v=0;v<n;v++){
            if(vis[v]==false&&G[u][v]!=inf){
                if(d[v]>d[u]+G[u][v]){
                    d[v]=d[u]+G[u][v];
                    pre[v].clear();
                    pre[v].push_back(u);
                }
                else if(d[u]+G[u][v]==d[v]){
                    pre[v].push_back(u);
                }
            }
        }
    }
}

void DFS(int v){
    if(v==st){
        tempPath.push_back(v);
        int tempCost=0;
        for(int i=tempPath.size()-1;i>0;i--){
            int id=tempPath[i],idNext=tempPath[i-1];
            tempCost+=cost[id][idNext];
        }
        if(tempCost<minCost){
            minCost=tempCost;
            path=tempPath;
        }
        tempPath.pop_back();
        return ;
    }
    tempPath.push_back(v);
    for(int i=0;i<pre[v].size();i++){
        DFS(pre[v][i]);
    }
    tempPath.pop_back();
}

int main(){
    scanf("%d%d%d%d",&n,&m,&st,&ed);
    int u,v;
    fill(G[0],G[0]+maxv*maxv,inf);///初始化图G
    fill(cost[0],cost[0]+maxv*maxv,inf);
    for(int i=0;i<m;i++){
        scanf("%d%d",&u,&v);
        scanf("%d%d",&G[u][v],&cost[u][v]);
        G[v][u]=G[u][v];
        cost[v][u]=cost[u][v];
    }
    Dijkstra(st);       ///Dijkstra算法入口
    DFS(ed);            ///获取最优路径
    for(int i=path.size()-1;i>=0;i--){
        printf("%d ",path[i]);          ///倒着输出路径上的结点
    }
    printf("%d %d\n",d[ed],minCost);    ///最短距离，最短距离上的最小花费
    return 0;
}



```


2,Dijkstra
```cpp

```










