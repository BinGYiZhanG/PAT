例题:
给定N个整数（可能有负数），从中选择K个数，使得这K个数之和恰好等于一个给定的整数X，如果有多种方案，选择它们中元素平方和最大的一个，数据保证这样的方案唯一.


### DFS



```cpp
#include <iostream>
#include <vector>
#include <cstdio>
#include <cstring>
using namespace std;
int n,k,p,maxfacSum=-1;
vector<int> fac,temp,ans;
int power(int x){
  int ans=1;
  for(int i=0;i<p;i++)
    ans*=x;
  return ans;
}

void init(){
  int tmp=0,i=0;
  while(tmp<=n){
    fac.push_back(tmp);
//    temp.push_back(tmp);
    tmp=power(++i);
  }
}

void DFS(int index,int nowK,int sum,int facSum){
  if(sum==n&&nowK==k){
    if(facSum>maxfacSum){
      maxfacSum=facSum;
      ans=temp;
    }
    return ;
  }
  if(nowK>k||sum>n) return ;
  if(index-1>=0){
//if(index-1>0){
    temp.push_back(index);
    DFS(index,nowK+1,sum+fac[index],facSum+index);
    temp.pop_back();
    DFS(index-1,nowK,sum,facSum);
  }
}

int main(){
  scanf("%d%d%d",&n,&k,&p);
  init();//没加
  DFS(fac.size()-1,0,0,0);
  if(maxfacSum==-1)
  printf("Impossible\n");
  else{
    printf("%d = %d^%d",n,ans[0],p);
    for(int i=1;i<ans.size();i++){
      printf(" + %d^%d",ans[i],p);
    }
  }
  return 0;
}
```












