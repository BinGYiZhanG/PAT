### 题意：
* 给定N个整数（可能有负数），从中选择K个数，使得这K个数之和恰好等于一个给定的整数X，如果有多种方案，选择它们中元素平方和最大的一个，数据保证这样的方案唯一.

### 问题：
* 题解代码不知道为什么要从尾到头遍历数组？

### WA代码，从0开始遍历数组（21分，超时代码）
```
#include <bits/stdc++.h>

using namespace std;

int N,K,P,flag,ansum=0;
vector<int> poww,lujing,ans;

bool cmp(){//判断是否可取
	for(int i=0;i<K;i++){
		if(ans[i]<lujing[i])
			return 1;
		else if(ans[i]>lujing[i])
			return 0;
	}
	return 0;
}

void DFS(int curN,int nowK){
    if(nowK>K||curN>N)
        return ;
    if(nowK==K&&curN==N){
        if(!flag)
            ans=lujing,flag=1;
        else{
            int sum=0;
            for(int i=0;i<(int)lujing.size();i++)
                sum+=lujing[i];
            if(sum>ansum){
                ans=lujing;
                ansum=sum;
            }
            else if(sum==ansum&&cmp())
                ans=lujing;
        }
        return ;
    }
    for(int i=0;i<(int)poww.size();i++){
        lujing.push_back(i);
        DFS(curN+poww[i],nowK+1);
        lujing.pop_back();
    }
}

int main(){
    scanf("%d%d%d",&N,&K,&P);
    int inum=1;
    flag=0;
    poww.push_back(inum);
    while(pow(inum,P)<=N){
        poww.push_back(pow(inum,P));
        inum++;
    }
    //for(int i=0;i<(int)poww.size();i++)
    //    printf("%d ",poww[i]);
    DFS(0,0);
	if(!flag)
		printf("Impossible");
	else{
		printf("%d = ",N);
		for(int i=0;i<K;i++){
			printf("%d^%d",ans[i],P);
			if(i!=K-1)
				printf(" + ");
		}
	}
    return 0;
}

```

### WA代码，27分代码（测试点5超时）
```
#include <bits/stdc++.h>

using namespace std;

int N,K,P,flag,ansum=0;
vector<int> poww,lujing,ans;

void DFS(int curindex,int curN,int nowK,int facsum){
    if(nowK>K||curN>N)
        return ;
    if(nowK==K&&curN==N){
        if(!flag){
			ans=lujing;
			flag=1;
			ansum=facsum;
		}
		else
		{
			if(ansum<facsum)
			{
				ansum=facsum;
				ans=lujing;
			}
		}
    }
    lujing.push_back(curindex);
    DFS(curindex,curN+poww[curindex],nowK+1,facsum+curindex);
    lujing.pop_back();
    if(curindex-1>=0)
        DFS(curindex-1,curN,nowK,facsum);
}

int main(){
    scanf("%d%d%d",&N,&K,&P);
    int inum=1;
    flag=0;
    poww.push_back(inum);
    while(pow(inum,P)<=N){
        poww.push_back(pow(inum,P));
        inum++;
    }
    //for(int i=0;i<(int)poww.size();i++)
    //    printf("%d ",poww[i]);
    DFS(poww.size()-1,0,0,0);
	if(!flag)
		printf("Impossible");
	else{
		printf("%d = ",N);
		for(int i=0;i<K;i++){
			printf("%d^%d",ans[i],P);
			if(i!=K-1)
				printf(" + ");
		}
	}
    return 0;
}

```

[题解二：从头到尾遍历数组](https://blog.csdn.net/qq_45228537/article/details/100182956)

### 题解，从尾到头遍历数组

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












