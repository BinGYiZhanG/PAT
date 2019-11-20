### 题意：
* 输出每个数的乘法结果

### 思路：
* 无需用```long long```型
* ```ansLen```记录乘法因子个数，```ansI```记录乘法因子的起点

```
#include <iostream>
#include <cmath>
#include <algorithm>
#include <cstdio>

using namespace std;


int main(){
  int n;
  scanf("%d",&n);
  int sqr=(int)sqrt(1.0*n),ansI=0,ansLen=0;
  for(int i=2;i<=sqr;i++){
    int temp=1,j=i;
    while(1){
      temp*=j;
      if(n%temp!=0)
        break;
      if(ansLen<j-i+1){
        ansLen=j-i+1;
        ansI=i;
      }
      j++;
    }
  }
  if(ansLen==0)
    printf("1\n%d\n",n);
  else{
    printf("%d\n",ansLen);
    for(int i=0;i<ansLen;i++){
      printf("%d",ansI+i);
      if(i<ansLen-1)
        printf("*");
    }
  }
  return 0;
}
```
