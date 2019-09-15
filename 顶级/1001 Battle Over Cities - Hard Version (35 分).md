* 在战争中，让所有的城市都由公路连接起来是至关重要的。如果一座城市被敌人占领，从那座城市到那座城市的所有公路都将关闭。为了保持其他城市的联系，我们必须以最低的成本维修一些高速公路。
* 另一方面，如果失去一座城市会让我们付出太多的代价来重建联系，我们必须更加关注这座城市。
* 在地图上标出了所有被毁的和剩下的高速公路，你应该指出我们最应该注意的城市。

### 输入：
每个输入文件包含一个测试用例
* N,城市总数；M,高速公路的数目
* 接下来M行，每行描述如下
  * ```City1 City2 Cost Status```，
    * ```Cost```是如果必要,修高速公路需要的花费
    * ```Status```，为0，以为着高速公路被摧毁，为1，意味着高速公路正在被使用
    
#### 注：保证在战争之前，所有城市连通

### 输出：

* 打印我们最应该保护的城市编号，也就是说，如果城市被敌人占领，重建所需要的最大花费.
* 如果要打印的城市不止一个，按城市编号的递增顺序输出它们，中间用一个空格隔开，但行尾没有多余的空格。如果根本不需要修复任何高速公路，只需输出0。

### Sample Input 1:
```
4 5
1 2 1 1
1 3 1 1
2 3 1 0
2 4 1 1
3 4 1 0
```

### Sample Output 1:
```
1 2
```

### Sample Input 2:
```
4 5
1 2 1 1
1 3 1 1
2 3 1 0
2 4 1 1
3 4 2 1
```

### Sample Output 2:
```
0
```

#### 29分代码，测试点3出错，

* 借鉴自[题解](https://blog.csdn.net/lianwaiyuwusheng/article/details/82758064)
* ```prim()```算法，计算除去被占领城市的最小生成树的总权值
* 同时对```prim()```算法的理解不深，有以下问题：
  * ```Dijsktra()算法```的```if(d[v]>d[u]+e[u][v])```  测试点2
  * ```prim()算法```的```if(d[v]>e[u][v])///更新集合到未被访问的点的最短路径```
  * 问题在于：把点加入最小生成树，和最短路是不同的



```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

const int inf=0x3f3f3f3f;
int e[510][510],d[510],cost[510];
bool vis[510];
int n,m;

void prim(int v){
    fill(vis,vis+510,false);
//    memset(vis,false,sizeof(vis));
    fill(d,d+510,inf);
    int s=v==n?1:v+1;
    //d[s]=d[v]=0;
    vis[v]=1;///置顶点v已访问，相当于结点v被占领
    for(int i=1;i<=n;i++)
        d[i]=e[s][i];///更新d数组

    for(int i=0;i<n;i++){
        int minn=inf,u=-1;
        for(int j=1;j<=n;j++){
            if(vis[j]==false&&minn>d[j])
            {
                minn=d[j];
                u=j;
            }
        }
        if(u==-1){
         ///   cost[v]=inf;
            break;
        }
        cost[v]+=d[u];
        vis[u]=true;
        for(int v=1;v<=n;v++){
            if(vis[v]==false){
               /// if(d[v]>d[u]+e[u][v])  测试点2
               if(d[v]>e[u][v])///更新集合到未被访问的点的最短路径
                d[v]=e[u][v];
            }
        }
    }
}

int main()
{
    int city1,city2,c,s;
    scanf("%d%d",&n,&m);

    fill(e[0],e[0]+510*510,inf);
    for(int i=0;i<m;i++){
        scanf("%d%d%d%d",&city1,&city2,&c,&s);
        if(s)   e[city1][city2]=e[city2][city1]=0;
        else    e[city1][city2]=e[city2][city1]=c;
    }
    int maxcost=0;
    for(int i=1;i<=n;i++){
        cost[i]=0;prim(i);
        if(cost[i]>maxcost) maxcost=cost[i];
    }

    if(maxcost==0)  printf("0");
    else{
        bool flag = 0;
		for (int i = 1; i <= n; ++i)
			if (cost[i] == maxcost) {
				printf("%s%d", flag ? " " : "", i);
				flag = 1;
			}

    }
    return 0;
}

```


#### 并查集的题解也写的很棒！

```
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>

using namespace std;

const inf=0x3f3f3f3f;

int father[510],cost[510];

struct Route{
    int c1,c2,cost,status;
    
    void read(){scanf("%d%d%d%d",&c1,&c2,&cost,&status);}
    
    ///重载小于，好的路径在前，cost递增
    bool operator <(cost Route& r){
        if(status!=r.status)
            return status>r.status;
        else
            return cost<r.cost;
    }
}route[300000];

int getroot(int n){
    if(root[n]==n)
        return n;
    else
        root[n]=getroot(root[n]);
}

int main(){
    int n,m,num;
    cin>>n>>m;
    
    for(int i=0;i<m;i++)    route[i].read();
    
    sort(route,route+m);
    
    int ans=0;
    
    
    
}

```





