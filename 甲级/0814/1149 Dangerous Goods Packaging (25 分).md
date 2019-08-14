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

```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <cmath>
#include <map>

using namespace std;

int main(){
    int N,M;
    scanf("%d%d",&N,&M);
    map<int,vector<int> > mp;
    for(int i=0;i<N;i++){
        int a,b;
        scanf("%d%d",&a,&b);
        mp[a].push_back(b);
        mp[b].push_back(a);
    }

    for(int i=0;i<M;i++){
        int cnt=0,flag=0,a[100000]={0};
        scanf("%d",&cnt);
        vector<int> v(cnt+1);
        for(int j=0;j<cnt;j++){
            scanf("%d",&v[j]);
            a[v[j]]=1;
        }

        for(int j=0;j<cnt;j++){
            for(int k=0;k<mp[v[j]].size();k++){
                if(a[mp[v[j]][k]]==1)
                    flag=1;
            }
        }
        if(flag)
            printf("No\n");
        else
            printf("Yes\n");
    }
    return 0;
}

```
