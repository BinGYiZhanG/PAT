### 建立二叉树
### 知识点
* 二叉树的中序遍历是有序的


```cpp
#include <iostream>
#include <cstdio>
#include <queue>
#include <algorithm>
using namespace std;

struct node{
    int data;
    int ld,rd;
}nd[110];
int in[110];

int num=0,n;
void inOrder(int index){
    if(index==-1)
        return ;
    inOrder(nd[index].ld);
    nd[index].data=in[num++];
    inOrder(nd[index].rd);
}

void levelOrder(){
    queue<int> q;
    q.push(0);
    num=0;
    while(!q.empty()){
        int tp=q.front();
        q.pop();

        num++;
        printf("%d",nd[tp].data);
        if(num<n)
            printf(" ");
        if(nd[tp].ld!=-1)
            q.push(nd[tp].ld);
        if(nd[tp].rd!=-1)
            q.push(nd[tp].rd);
    }
}

int main()
{
    int lf,rt;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d%d",&lf,&rt);
        if(lf!=-1)
            nd[i].ld=lf;
        else
            nd[i].ld=-1;

        if(rt!=-1)
            nd[i].rd=rt;
        else
            nd[i].rd=-1;
    }

    for(int i=0;i<n;i++)
        scanf("%d",&in[i]);
    sort(in,in+n);
    inOrder(0);
    levelOrder();

    return 0;
}


```

