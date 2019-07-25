给出一个根为R，每一个树节点$T_{i}$的权值为$W_{i}$。一条从R到L的权值被定义为所有从R到任意叶节点L的所有结点的权值之和。<br>

现在给出任意权值树，你应该发现它们中所有与给定值相等的路径。例如，让我们考虑在树中以下路径：对于每一个结点，上面的数是一个两位数的结点ID，
并且下面的数是一个节点的权值。假定被给数是24，然后存在四条有着相同给定权值的不同路径：{10 5 2 7}, {10 4 10}, {10 3 3 6 2} and {10 3 3 6 2}, 在图上是连接着红边的。

### 输入：
每一个输入文件包含一个测试用例。<br>
N,树的结点总数；M，非叶节点的数量；S，$[0,2^{30}]$，给出的权值。下一个包含N个正数树节点$T_{i}$的权值$W_{i}$，然后M行的格式如下：<br>

```
ID K ID[1] ID[2] ... ID[K]
```

```ID```是一个代表给出的非叶节点的二位数；K，是子节点的数量，随后，是它们的两位数```ID```，根节点ID是```00```。

### 输出：
每一个测试用例，打印所有的路径按照递减序。<br>

每一条路径打印从根节点到叶节点按照顺序。<br>
Note:序列${A_{1},A_{2},...,A_{n}}$比序列${B_{1},B_{2},...,B_{m}}$大，如果存在$1\leq k<$min{n,m}使得$A_{i}=B_{i}$对于i=1,...,k,并且$A_{k+1}>B_{k+1}$。<br>


### 注意点：
* 题中所说按递减序打印，是在输出每层结点时所说（看题图，对照输出即可），
* 路径必须是根节点到叶节点，也就是说得加一个对于最后结点是否为叶节点的判断
* DFS在大于S时，要返回

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>

using namespace std;

int N,M,S;
int weight[110],path[110];
vector<int> node[110];
int num=0;

///题中的路径按递减序：是每一层的结点，按权值由大到小排列
bool cmp(int a,int b){
    return weight[a]>weight[b];
}

void DFS(int index,int tmpindex,int sum){
    if(sum>S)///DFS常规操作
        return ;
    if(sum==S){
        if(node[index].size()!=0)///审题不清，必须得到叶节点才可以输出（一开始没加）
            return ;
        for(int i=0;i<tmpindex;i++){
            if(i!=tmpindex-1)
                printf("%d ",weight[path[i]]);
            else
                printf("%d",weight[path[i]]);
        }
        printf("\n");
        return ;
    }
    for(int i=0;i<(int)node[index].size();i++){
        int child=node[index][i];
        path[tmpindex]=child;
        DFS(child,tmpindex+1,sum+weight[child]);
    }
}

int main(){
    scanf("%d%d%d",&N,&M,&S);
    for(int i=0;i<N;i++){
        scanf("%d",&weight[i]);
    }
    int ID,K,tmpID;
    for(int i=0;i<M;i++){
        scanf("%d%d",&ID,&K);
        for(int i=0;i<K;i++){
            scanf("%d",&tmpID);
            node[ID].push_back(tmpID);
        }
        sort(node[ID].begin(),node[ID].end(),cmp);
    }
    path[0]=0;
    DFS(0,1,weight[0]);
    return 0;
}
```
