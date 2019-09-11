
#### 要点：
* ```node* newnode(int data){ ```中的```node* Node=new node;```，最后没```()```,
*  ```if(root->data>data){```插入左子树，```LL```型，与```LR```型
* ```else```插入右子树，```RR```型，与```RL```型

```
#include <bits/stdc++.h>

using namespace std;

struct node{
    int data,height;
    node *lchild,*rchild;
};

node* newnode(int data){
    node* Node=new node;
    Node->data=data;
    Node->height=1;
    Node->lchild=Node->rchild=NULL;
    return Node;
}

int getHeight(node* root){
    if(root==NULL)
        return 0;
    return root->height;
}

void updateHeight(node* root){
    root->height=max(getHeight(root->lchild),getHeight(root->rchild))+1;
}

int getBalanceFractor(node* root){
    return getHeight(root->lchild)-getHeight(root->rchild);
}

void L(node* &root){
    node* tmp=root->rchild;
    root->rchild=tmp->lchild;
    tmp->lchild=root;
    updateHeight(root);
    updateHeight(tmp);
    root=tmp;
}

void R(node* &root){
    node* tmp=root->lchild;
    root->lchild=tmp->rchild;
    tmp->rchild=root;
    updateHeight(root);
    updateHeight(tmp);
    root=tmp;
}

void insert_(node* &root,int data){
    if(root==NULL){
        root=newnode(data);
        return ;
    }

    if(root->data>data){
        insert_(root->lchild,data);
        updateHeight(root);
        if(getBalanceFractor(root)==2){
            if(getBalanceFractor(root->lchild)==1){
                R(root);
            }
            else if(getBalanceFractor(root->lchild)==-1){
                L(root->lchild);
                R(root);
            }
        }
    }

    else{
        insert_(root->rchild,data);
        updateHeight(root);
        if(getBalanceFractor(root)==-2){
            if(getBalanceFractor(root->rchild)==-1){
                L(root);
            }
            else if(getBalanceFractor(root->rchild)==1){
                R(root->rchild);
                L(root);
            }
        }
    }
}

int isComplete=1,after=0;
vector<int> levelOrder(node *tree){
    vector<int> v;
    queue<node *> q;
    q.push(tree);

    while(!q.empty()){
        node *tmp=q.front();
        q.pop();

        v.push_back(tmp->data);
        if(tmp->lchild!=NULL){
            if(after)   isComplete=0;
            q.push(tmp->lchild);
        }
        else{
            after=1;
        }

        if(tmp->rchild!=NULL){
            if(after)   isComplete=0;
            q.push(tmp->rchild);
        }
        else{
            after=1;
        }
    }

    return v;
}


int main()
{
    int n,tmp;

    scanf("%d",&n);
    node* tree=NULL;
    for(int i=0;i<n;i++){
        scanf("%d",&tmp);
        insert_(tree,tmp);
    }

    vector<int> v=levelOrder(tree);

    for(int i=0;i<(int)v.size();i++){
        if(i)
            printf(" ");
        printf("%d",v[i]);
    }

    printf("\n%s",isComplete?"YES":"NO");


    return 0;
}

```

