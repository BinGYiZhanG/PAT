## 1，拓扑排序

```cpp
vector<int> G[maxv];
int n,m,inDegree[maxv];

bool topologicalSort(){
  int num=0;
  queue<int> q;
  for(int i=0;i<n;i++)
    if(inDegree[i]==0)///将所有入度为0的顶点入队
      q.push(i);
      
  while(!q.empty()){
    int u=q.front();
    q.pop();
    for(int i=0;i<G[u].size();i++){
      int v=G[u][i];      ///u的后继结点v
      inDegree[v]--;      ///顶点v的入度减1
      if(inDegree[v]==0)    ///顶点v的入度减为0，则入队
        q.push(v);
        
    }
    G[u].clear();
    num++;
  }
  if(num==n)  return true;///加入拓扑排序的顶点数为n，说明拓扑排序成功
  else return false;///
}


```

[](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07031631.png)
## 2，计算数组ve（最早发生时间），

[](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07031633.png)
```cpp
stack<int> topOrder;
//拓扑排序，顺便求ve数组
bool topologicalSort(){
  queue<int> q;
  for(int i=0;i<n;i++)
    if(inDegree[i]==0)
      q.push(i);
      
  while(!q.empty()){
    int u=q.front();
    q.pop();
    topOrder.push(u);
    for(int i=0;i<G[u].size();i++){
      int v=G[u][i].v;
      inDegree[v]--;
      if(inDegree[v]==0)
        q.push(v);
      //用ve[i]来更新u的所有后继结点v
      if(ve[u]+G[u][i]>ve[e]){
        ve[v]=ve[u]+G[u][i].w;
      }
    }
  }
  if(topOrder.size()==n)  return true;
  else  return false;
}
```

## 3,计算数组vl（最迟发生时间）
![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07031639.png)

```cpp
fill(vl,vl+n,ve[n-1]);///vl数组初始化，初始值为终点的ve值

//直接使用topOrder出栈即为逆拓扑序列，求解vl数组
while(!topOrder.empty()){
  int u=topOrder.top();
  topOrder.pop();
  for(int i=0;i<G[u].size();i++){
    int v=G[u][i].v;
    ///用u的所有后继结点v的vl值来更新vl[u]
    if(vl[v]-G[u][i].v<vl[u])
      vl[u]=vl[v]-G[u][i].w;
  }
}
```

## 计算关键路径

```cpp
///关键路径，不是有向无环图返回-1，否则返回关键路径长度
int CriticalPath(){
  memset(ve,0,sizeof(ve));
  if(topologicalSort()==false)
    return -1;///不是有向无环图，返回-1
  fill(vl,vl+n,ve[n-1]);///vl数组初始化，初始值为终点的ve值

  //直接使用topOrder出栈即为逆拓扑序列，求解vl数组
  while(!topOrder.empty()){
  int u=topOrder.top();
    topOrder.pop();
    for(int i=0;i<G[u].size();i++){
      int v=G[u][i].v;
      ///用u的所有后继结点v的vl值来更新vl[u]
      if(vl[v]-G[u][i].v<vl[u])
        vl[u]=vl[v]-G[u][i].w;
    }
  }
  
  //遍历邻接表的所有边，计算活动的最早开始时间e和最迟开始时间l
  for(int u=0;u<n;u++){
    for(int i=0;i<G[u].size();i++){
      int v=G[u][i].v,w=G[u][i].w;
      //活动的最早开始时间e和最迟开始时间l
      int e=ve[u],l=vl[v]-w;
      //如果e==l,说明活动u->v是关键活动
      if(e==l)
        printf("%d->%d\n",u,v);//输出关键活动
    }
  }
  return ve[n-1];//返回关键路径长度
}



```
![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07031652.png)


# 动态规划  --   DAG最长路








