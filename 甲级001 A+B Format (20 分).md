
### 坑点：
### 如果是小于1000的数的话，必须得按原样输出，如果是在开头的话，也就是不能有前导0
```cpp
#include <iostream>

using namespace std;

int main(){
    int a,b;
    scanf("%d%d",&a,&b);
    int sum=a+b;
    if(sum<1000&&sum>-1000){
        printf("%d\n",sum);
    }
    else if(sum<1000000&&sum>-1000000){
        printf("%d,%03d\n",sum/1000,abs(sum%1000));
    }
    else
        printf("%d,%03d,%03d\n",sum/1000000,abs(sum/1000%1000),abs(sum%1000));
    return 0;
}
```
