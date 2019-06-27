
```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <string>
#include <algorithm>
using namespace std;

const int maxn=100010;

int pnums[maxn],cnums[maxn];

int main(){
    int pnum,cnum;
    scanf("%d",&pnum);
    for(int i=0;i<pnum;i++)
        scanf("%d",&pnums[i]);
    sort(pnums,pnums+pnum);
    scanf("%d",&cnum);
    for(int i=0;i<cnum;i++)
        scanf("%d",&cnums[i]);
    sort(cnums,cnums+cnum);
    int sum=0;
    int i,j;
    i=0,j=0;
    while(i<pnum&&j<cnum){
        if(pnums[i]<0&&cnums[j]<0)
            sum+=pnums[i]*cnums[j];
        i++,j++;
    }
    i=pnum-1,j=cnum-1;
    while(i>=0&&j>=0){
        if(pnums[i]>0&&cnums[j]>0)
            sum+=pnums[i]*cnums[j];
        i--,j--;
    }
    printf("%d\n",sum);
    return 0;
}



```
