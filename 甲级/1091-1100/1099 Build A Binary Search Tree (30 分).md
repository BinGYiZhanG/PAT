### 建立二叉树
### 知识点
* 二叉树的中序遍历是有序的


```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;

int in[110];
bool isroot[110];
struct node{
    int data;
    int lchild,rchild;
}nd[110];
int n,num;

void inOrder(int root){
    if(root==-1)
        return ;
    inOrder(nd[root].lchild);
    nd[root].data=in[num++];
    inOrder(nd[root].rchild);
}

void Level_order(int root){
    queue<int> q;
    num=0;
    q.push(root);
    while(!q.empty()){
        int top=q.front();q.pop();
        printf("%d",nd[top].data);
        num++;
        if(num<n){
            printf(" ");
        }
        if(nd[top].lchild!=-1)
            q.push(nd[top].lchild);
        if(nd[top].rchild!=-1)
            q.push(nd[top].rchild);
    }
}


int main()
{
    int lf,rt;
    scanf("%d",&n);
    memset(isroot,0,sizeof(isroot));
    for(int i=0;i<n;i++){
        scanf("%d%d",&lf,&rt);
        nd[i].lchild=lf;
        if(lf!=-1)
            isroot[lf]=true;
        nd[i].rchild=rt;
        if(rt!=-1)
            isroot[rt]=true;
    }
    for(int i=0;i<n;i++){
        scanf("%d",in+i);
    }
    int root=-1;
    for(int i=0;i<n;i++){
        if(isroot[i]==false){
            root=i;
            break;
        }
    }
    sort(in,in+n);
    num=0;
    inOrder(root);
    Level_order(root);
    return 0;
}

```

