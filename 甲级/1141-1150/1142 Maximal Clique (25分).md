一个clique是一个无向图的点的集合在clique中的每两个点是邻接的。一个最大clique是一个通过包含邻接点不能进行扩展的clique。<br>
现在你的工作是判断一个被给的点集合是否是一个最大clique。<br>

### 输入
对于每个样例，<br>
* 第一行，Nv，图中的顶点数目（Nv小于等于200）；Ne，图中的无向边数。
* 接下来Ne行，是每条边，边的结点序号是从1~Nv。
在图之后，输入M，是M个需要判断的clique<br>
接下来M行,第一个数是K，代表每个clique的顶点数，然后是其中的点<br>

### 输出：
对于M个查询，
* 如果是```maximal clique```,输出```Yes```
* 如果不是```maximal clique```，但是一个```clique```,输出```Not Maximal```
* 如果不是```clique```,输出```Not a Clique```

### Sample Input:
```
8 10
5 6
7 8
6 4
3 6
4 5
2 3
8 2
2 7
5 3
3 4
6
4 5 4 3 6
3 2 8 7
2 2 3
1 1
3 4 3 6
3 3 2 1
```
### Sample Output:
```
Yes
Yes
Yes
Yes
Not Maximal
Not a Clique
```

* 代码注意：判断```Not a Maximal```与```Yes```时，有如下代码，含义是：结点```j```与集合中的点均相连，则，判断为```Not a Maximal```，也就是可以添加进```clique```
```
for(int k=0;k<nums;k++)
    //if(e[j][v[k]]==1||e[v[k]][j]==1){///存在相连
    //if(e[v[k]][j]==1){
    //    flag1=false;
     //   break;
    //}
{
    if(e[v[k]][j]==0){
        break;
    }
    if(k==nums-1)
        flag1=false;
}
```

```
#include <bits/stdc++.h>
using namespace std;

int n,m;
int e[201][201];
int v[201];

int main()
{
    int a,b;
    fill(e[0],e[0]+201*201,0);
    scanf("%d%d",&n,&m);
    for(int i=0;i<m;i++){
        scanf("%d%d",&a,&b);
        e[a][b]=e[b][a]=1;
    }
    int q;
    scanf("%d",&q);
    set<int> st;//作用：判断要判断的点是否在集合中
    for(int i=0;i<q;i++){
        int nums;
        st.clear();
        scanf("%d",&nums);///顶点总数
        for(int j=0;j<nums;j++){
            scanf("%d",&v[j]);
            st.insert(v[j]);
        }
        bool flag=true;//判断是否是一个cliuqe
        for(int j=0;j<nums;j++){
            for(int k=j+1;k<nums;k++){
                if(e[v[j]][v[k]]==0)
                {
                    flag=false;
                    break;
                }
            }
        }
        if(flag==false)
        {
            printf("Not a Clique\n");
            continue;
        }
        bool flag1=true;
        //接下来判断是否是maxclique
        for(int j=1;j<=n;j++)
            if(st.count(j)<=0)///该集合中没有这个点
            for(int k=0;k<nums;k++)
                //if(e[j][v[k]]==1||e[v[k]][j]==1){///存在相连
                //if(e[v[k]][j]==1){
                //    flag1=false;
                 //   break;
                //}
            {
                if(e[v[k]][j]==0){
                    break;
                }
                if(k==nums-1)
                    flag1=false;
            }
        if(flag1==true)
            printf("Yes\n");
        else
            printf("Not Maximal\n");
    }
    return 0;
}

```
