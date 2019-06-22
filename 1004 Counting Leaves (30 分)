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

坑点：总是想着在BFS的while循环内依靠一个layers来记录层数，这明显是不可能的，因为一层可能有多个节点，不可能只通过一个layers来记录

AC代码:
#include <bits/stdc++.h>

using namespace std;

const int maxn=100+10;
int n,m;
vector<int> G[maxn];
int h[maxn];///每层有多少个叶结点
int leaf[maxn];
int maxh=0;

void BFS(){
    queue<int> q;
    q.push(1);
 //   int layers=2///控制层数
    while(!q.empty()){
        int id=q.front();
        q.pop();
        maxh=max(maxh,h[id]);
        if(G[id].size()==0)
            leaf[h[id]]++;
        for(int i=0;i<G[id].size();i++){
            int child=G[id][i];
            h[child]=h[id]+1;
            q.push(child);

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
    h[1]=1;
    BFS();
    for(int i=1;i<=maxh;i++){
        if(i==1)
			printf("%d", leaf[i]);
		else
			printf(" %d", leaf[i]);
    }
}
