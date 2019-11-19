
### 题意：
* 去掉一个链表中权值重复的结点，即将重复结点放在链表的最后

### 思路：
* 加一个```order```变量，根据结点是否重复，规定结点的位置

```
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
using namespace std;

const int maxn=100010;
const int TABLE=10000001;
struct Node{
  int address,next,data;
  int order;///根据结点是否重复，设置结点的位置,0~maxn：不重复结点的位置，maxn~：重复结点的位置
}node[maxn];

bool isExist[TABLE]={false};
bool cmp(Node a,Node b){
  return a.order<b.order;
}

int main(){
  memset(isExist,false,sizeof(isExist));
  for(int i=0;i<maxn;i++)
    node[i].order=2*maxn;//一开始将结点都设置成重复结点的位置
  int begin_,n;
  int address;
  scanf("%d%d",&begin_,&n);
  for(int i=0;i<n;i++){
    scanf("%d",&address);
    scanf("%d%d",&node[address].data,&node[address].next);
    node[address].address=address;
  }
  int countValid=0,countRemoved=0,p=begin_;///cntValid：记录合法结点数，cntRemoved：记录重复结点数
  while(p!=-1){
    if(isExist[abs(node[p].data)]==false){
      isExist[abs(node[p].data)]=true;
      node[p].order=countValid++;///将合法结点的order设置成0~maxn
    }
    else{
      node[p].order=maxn+countRemoved++;j///非法结点的order设置成maxn~向后
    }
    p=node[p].next;
  }
  int count_=countRemoved+countValid;
  sort(node,node+maxn,cmp);
  for(int i=0;i<count_;i++){
//  for(int i=0;i<maxn;i++){      
    if(i!=countValid-1&&i!=count_-1){
      printf("%05d %d %05d\n",node[i].address,node[i].data,node[i+1].address);
    }
    else{
      printf("%05d %d -1\n",node[i].address,node[i].data);
    }
  }
  return 0;
}


```



