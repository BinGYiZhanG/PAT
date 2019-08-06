
24分代码
![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/08061959.png)
和答案唯一区别就在于  判断```while```循环的变量,

```cpp
#include <iostream>
#include <cstring>
#include <cstdio>

using namespace std;

struct Node{
    bool flag;
    int address,next_;
    char data;
}node[100000];

int main(){
    for(int i=0;i<100000;i++){
        node[i].flag=false;
    }
    int st1,st2,n;
    scanf("%d%d%d",&st1,&st2,&n);
    for(int i=0;i<n;i++){
        int addr,nex;
        char id;

        scanf("%d %c %d",&addr,&id,&nex);
        node[addr].address=addr;
        node[addr].data=id;
        node[addr].next_=nex;
    }

    int p1=st1;
    while(node[p1].next_!=-1){
        node[p1].flag=true;
        p1=node[p1].next_;
       // printf("OK\n");
    }
    p1=st2;
    while(node[p1].next_!=-1){
        if(node[p1].flag==true)
            break;
        p1=node[p1].next_;
    }

    if(node[p1].next_==-1)
        printf("-1\n");
    else
        printf("%05d\n",node[p1].address);
    return 0;
}

```

我感觉这是正常人思维

```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxn=100010;
struct Node{
    char data;
    int next;
    bool flag;
}node[maxn];

int main(){
    for(int i=0;i<maxn;i++)
        node[i].flag=false;
    int s1,s2,n;
    scanf("%d%d%d",&s1,&s2,&n);
    int address,next;
    char data;
    for(int i=0;i<n;i++){
        scanf("%d %c %d",&address,&data,&next);
        node[address].data=data;
        node[address].next=next;
    }
    int p;
    for(p=s1;p!=-1;p=node[p].next)
        node[p].flag=true;
    for(p=s2;p!=-1;p=node[p].next)
        if(node[p].flag)
            break;
    if(p!=-1)
        printf("%05d\n",n);
    else
        printf("-1\n");
    return 0;
}
```
