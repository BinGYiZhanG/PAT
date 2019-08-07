
我自己写的，虽说不对，但是说明我对```DFS```有了一定理解
```cpp
#include <cstdio>
#include <cstring>
#include <iostream>
#include <vector>

using namespace std;

int n,m,s;
int id[110];
vector<int> vec[110];///每个结点包含的叶节点
vector<int> tempath;///记录路径
bool vis[110];

void DFS(int vispos,int value){
    vis[vispos]=true;
    if(value==s){
        for(int i=0;i<(int)tempath.size();i++){
            if(i!=0)
                printf(" ");
            printf("%d",id[tempath[i]]);
        }
        tempath.pop_back();
        return ;
    }
    for(int i=0;i<(int)vec[vispos].size();i++){
        if(vis[vispos]==false)
            DFS(vec[vispos][i],value+id[vispos]);
    }
    return ;
}


int main(){
    scanf("%d%d%d",&n,&m,&s);
    for(int i=0;i<n;i++){
        scanf("%d",&id[i]);
    }

    for(int i=0;i<m;i++){
        int fa,num,child;
        scanf("%d%d",&fa,&num);
        for(int j=0;j<num;j++){
            scanf("%d",&child);
            vec[fa].push_back(child);
        }
    }

    tempath.push_back(0);
    DFS(0,0);///从0号结点开始走，一开始的价值是id[0]
}
```

