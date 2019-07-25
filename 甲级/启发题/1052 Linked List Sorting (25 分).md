一个链表包含一系列的结构，其在内存上不一定是连续的。我们假定每一个结构包含一个正数```key```和一个指向下一个结构的```Next```指针。现在给出一个链表，你应该对它们的键值按照递增序排序。

### 输入：
每一个输入文件包含一个测试用例。对于每一个例子，<br>
第一行，N，and，头结点的地址，<br>
N，在内存中节点个数；节点的地址是一个5位正整数。-1代表NULL。<br>
接下来的N行格式如下：
```
Address Key Next
```
```Address```是内存中的结点地址；```Key```是一个整数在$[-10^{5},10^{5}]$，```Next```是下一个结点的地址。保证所有的键值是唯一的，从链表头结点开始没有环形成。

### 输出：
对于每一个测试用例，输出的格式与输入的格式类似，<br>
N，链表中的结点总数，所有结点被排序。


#### 24分代码

![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07250806.png)
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
using namespace std;

const int maxn=100010;
struct Node{
    int address,data,next;
    bool flag;
}node[maxn];

bool cmp(Node a,Node b){
    if(a.flag==false||b.flag==false)
        return a.flag>b.flag;
    else
        return a.data<b.data;
}

int main(){
    int N,st;
    int addre;
    scanf("%d%d",&N,&st);
    for(int i=0;i<N;i++){
        scanf("%d",&addre);
        scanf("%d%d",&node[addre].data,&node[addre].next);
        node[addre].address=addre;
    }

    int p=st;
    int cnt=0;///记录
    while(p!=-1){
        node[p].flag=true;
        p=node[p].next;
        cnt++;
    }

    sort(node,node+maxn,cmp);///对所有maxn排序，而非N排序

    printf("%d %05d\n",cnt,node[0].address);

    for(int i=0;i<cnt;i++){
        if(i!=cnt-1)
        printf("%05d %d %05d\n",node[i].address,node[i].data,node[i+1].address);
        else
        printf("%05d %d -1\n",node[i].address,node[i].data);
    }
    return 0;
}

```



AC代码，加上对```cnt==0```的的判断

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
using namespace std;

const int maxn=100010;
struct Node{
    int address,data,next;
    bool flag;
}node[maxn];

bool cmp(Node a,Node b){
    if(a.flag==false||b.flag==false)
        return a.flag>b.flag;
    else
        return a.data<b.data;
}

int main(){
    int N,st;
    int addre;
    scanf("%d%d",&N,&st);
    for(int i=0;i<N;i++){
        scanf("%d",&addre);
        scanf("%d%d",&node[addre].data,&node[addre].next);
        node[addre].address=addre;
    }

    int p=st;
    int cnt=0;///记录
    while(p!=-1){
        node[p].flag=true;
        p=node[p].next;
        cnt++;
    }

    if(cnt==0){
        printf("0 -1\n");
    }
    else{
        sort(node,node+maxn,cmp);

        printf("%d %05d\n",cnt,node[0].address);
        for(int i=0;i<cnt;i++){
            if(i!=cnt-1)
            printf("%05d %d %05d\n",node[i].address,node[i].data,node[i+1].address);
            else
            printf("%05d %d -1\n",node[i].address,node[i].data);
        }
    }
    return 0;
}

```






