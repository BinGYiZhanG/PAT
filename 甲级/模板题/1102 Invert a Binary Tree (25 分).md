### 翻转二叉树
* 注意数据读入，处理
* 注意如何翻转
* 注意根节点的确定
* 注意遍历终止条件


```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <queue>

using namespace std;

struct node{
    int lchild,rchild;
}nd[22];
int n;
bool notRoot[22];

int num = 0;
void print(int id) {
	printf("%d", id);
	num++;
	if (num < n)
		printf(" ");
	else
		printf("\n");
}

void inOrder(int root) {
	if (root == -1)
		return;
	inOrder(nd[root].lchild);
	print(root);
	inOrder(nd[root].rchild);
}

void BFS(int root) {
	queue<int> q;
	q.push(root);
	while (!q.empty()) {
		int now = q.front();
		q.pop();
		print(now);
		if (nd[now].lchild != -1)
			q.push(nd[now].lchild);
		if (nd[now].rchild != -1)
			q.push(nd[now].rchild);
	}
}

void postOrder(int root){
    if(root==-1)///一开始想不通为什么root是-1,
        return ;
    postOrder(nd[root].lchild);
    postOrder(nd[root].rchild);
    swap(nd[root].lchild,nd[root].rchild);
}


void strtoint(int id,char c1,char c2){
    if(c1=='-')
        nd[id].lchild=-1;
    else{
        nd[id].lchild=c1-'0';
        notRoot[c1-'0']=true;
    }

    if(c2=='-')
        nd[id].rchild=-1;
    else {
        nd[id].rchild=c2-'0';
        notRoot[c2-'0']=true;
    }
}

int findroot(){
    for(int i=0;i<n;i++){
        if(notRoot[i]==false)
            return i;
    }
}

int main()
{
    memset(notRoot,0,sizeof(notRoot));
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        char c1,c2;
        //scanf("%c %c",&c1,&c2);
        scanf("%*c%c %c",&c1,&c2);
        strtoint(i,c1,c2);
    }
    int root=findroot();
    postOrder(root);
	BFS(root);
	num = 0;
	inOrder(root);
	return 0;
}

```
