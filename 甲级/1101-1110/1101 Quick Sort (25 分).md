题意：查询在数组满足条件 ```大于左边的元素，小于右边的元素``` 的元素数

* 遍历n个数，判断每个数左右两边的数是否符合，此数左边的数都小于此数，此数右边的数都大于此数

* 注意格式输出，当不存在时，该如何输出
```
if(cnt==0){
        printf("\n");///注意格式输出
    }
```

```cpp

#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;

const int maxn=100010;
int a[maxn],b[maxn];

int main()
{
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d",a+i);
    }
    int cnt=0;
    for(int i=0;i<n;i++){
        int lf=i-1,rt=i+1;
        bool lflag=true,rflag=true;
        while(lf>=0){
            if(a[lf]>a[i]){
                lflag=false;
                break;
            }
            lf--;
        }
        if(lflag==false){
            continue;
        }

        while(rt<n){
            if(a[rt]<a[i]){
                rflag=false;
                break;
            }
            rt++;
        }
        if(rflag==false){
            continue;
        }
        b[cnt++]=a[i];
    }
    if(cnt==0){
        printf("\n");///注意格式输出
    }
    else{
        sort(b,b+cnt);
        printf("%d\n",cnt);
        for(int i=0;i<cnt;i++){
            if(i==0)
                printf("%d",b[i]);
            else
                printf(" %d",b[i]);
        }
    }
    return 0;
}

```
