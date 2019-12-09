### 输入
* 第一行，N，不相容货物的对数，M，需要被运输的货物数列表
* 以下两块是
  * 第一块，N对不相容的货物，
  * 第二块，M条需要被运输的货物
  * 格式如下：
  ```K G[1] G[2] ... G[K]```

```K```是货物数，```G[i]```是货物的ID，为了简化问题，每种货物用5位整数ID代替

### 输出

* 如果没有不相容的货物，输出```Yes```
* 否则，输出```No```

### 思路 
* 每一种液体可能与多种液体不相容,，所以在记录不相容物品时，不能写成如下形式
```
//int a_1[maxn_1],a_2[maxn_1];//对应的不相容物品
//每一种液体可能与多种液体不相容,下述代码错误,
//for(int i=0;i<N;i++){
//    scanf("%d%d",&a_1[i],&a_2[i]);
//}

```
* ```map<int,vector<int> > m;```记录每种物品的不相容物品的列表

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn_1=110;
//int a_1[maxn_1],a_2[maxn_1];//对应的不相容物品

int main(){
    int N,M;
    scanf("%d%d",&N,&M);
    //每一种液体可能与多种液体不相容,下述代码错误,
    //for(int i=0;i<N;i++){
    //    scanf("%d%d",&a_1[i],&a_2[i]);
    //}

    map<int,vector<int> > m;//记录每种物品的不相容物品的列表
    for(int i=0;i<N;i++){
        int t1,t2;
        scanf("%d%d",&t1,&t2);
        m[t1].push_back(t2);
        m[t2].push_back(t1);
    }
    while(M--){
        int cnt,flag=0,a[100000]={0};
        scanf("%d",&cnt);
        vector<int> vec(cnt);
        for(int j=0;j<cnt;j++){
            scanf("%d",&vec[j]);
            a[vec[j]]=1;
        }
        for(int i=0;i<vec.size();i++){
        //统计该箱货物
            for(int j=0;j<m[vec[i]].size();j++){
            //在不相容物品中，寻找该箱物品的每一个（已利用map变量m建立关系不相容物品的关系），确定在该箱中是否出现
                if(a[m[vec[i]][j]]==1) flag=1;///判断该物品的不相容物品列表中，是否存在冲突
            }
        }
        if(flag){
            printf("No\n");
        }
        else{
            printf("Yes\n");
        }
    }

    /*
    while(M--){
        int cnt,tmp;
        set<int> pro;
        scanf("%d",&cnt);
        for(int j=0;j<cnt;j++){
            scanf("%d",&tmp);
            pro.insert(tmp);
        }
        int i;
        int flag=0;
        for(i=0;i<N;i++){
            if(pro.count(a_1[i])&&pro.count(a_2[i])){
                printf("No\n");
                flag=1;
            }
        }
        if(!flag){
            printf("Yes\n");
        }
    }
    */

}
```
