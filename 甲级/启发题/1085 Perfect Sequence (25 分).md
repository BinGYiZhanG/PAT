给出一个正数序列和另一个正数p，这个序列据说是一个 完美序列 如果M<=m*p M和m是序列里的最大最小数，分别的。
现在给出一个序列和一个参数p，你应该找到一个序列中尽可能多的数组成一个完美序列。
输入：
N，序列中的数字个数，p，是一个参数，N个正数，大小不超过10^9
输出：
输出所选序列的最大数


### 非满分代码
![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07172324.png)
```cpp

#include <iostream>
#include <algorithm>
#include <cstdio>
#include <cmath>
using namespace std;

const int maxn=100010;
int a[maxn];
int n,p;

int main(){
    scanf("%d%d",&n,&p);
    for(int i=0;i<n;i++){
        scanf("%d",a+i);
    }
    sort(a,a+n);
    int res=1;
    for(int i=0;i<n;i++){
        for(int j=i+1;j<n;j++){
            if((a[j]<=(long long)a[i]*p)){///long long型，测试点5正确
                res=max(res,j-i+1);///加1，测试点1,2,3，正确
            }
        }
    }
    printf("%d\n",res);
    return 0;
}
```

AC代码
### 说明while比for循环快
```cpp
#include <cstdio>
#include <algorithm>
using namespace std;
const int maxn=100010;
int main(){
  int n,p,a[maxn];
  scanf("%d%d",&n,&p);
  for(int i=0;i<n;i++){
    scanf("%d",&a[i]);
  }
  sort(a,a+n);
  int i=0,j=0,count=1;
  while(i<n&&j<n){
    while(j<n&&a[j]<=(long long)a[i]*p){
      count=max(count,j-i+1);
      j++;
    }
    i++;
  }
  printf("%d\n",count);
  return 0;
}
```
