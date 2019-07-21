给出3个整数A，B，C在$\left [ -2^{63},2^{63} \right ]$范围内，你应该判断A+B>C是否成立。
### 输入：
T，测试用例的个数；
接下来T行，每一行输入A，B，C
### 输出：
A+B>C，true；A+B<C，false。

```cpp
#include <iostream>
#include <cstdio>

using namespace std;

int main(){
  int T,tcase=1;
  scanf("%d",&T);
  while(T--){
    long long a,b,c;
    scanf("%lld%lld%lld",&a,&b,&c);
    long long res=a+b;
    bool flag;
    if(a>0&&b>0&&res<0)
      flag=true;
    else if(a<0&&b<0&&res>=0)
      flag=false;
    else if(res>C)
      flag=true;
    else
      flag=false;
    if(flag)
      printf("Case %d: true\n",tcase++);
    else
      printf("Case %d: false\n",tcase++);
  }
  return 0;
}

```










