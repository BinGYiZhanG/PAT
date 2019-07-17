

```cpp
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <string>
#include <math.h>
using namespace std;

int n;
//插入排序
void insort(int a[],int b[]){
    int key=0;
    for(int i=2;i<=n;i++){
        sort(a,a+i);//从0~n的插入排序的操作
        if(key){
            printf("Insertion Sort\n");
            printf("%d",a[0]);
            for(int j=1;j<n;j++)
                printf(" %d",a[j]);
            return ;
        }
        if(equal(a,a+n,b))
            key=1;
    }
}

void mesort(int a[],int b[]){
    int key=0;
    for(int i=2;;i*=2){
        for(int j=0;j<n;j+=i){
            sort(a+j,a+(i+j<n?j+i:n));
        }
        if(key){
            printf("Merge Sort\n");
            printf("%d",a[0]);
            for(int j=1;j<n;j++){
                printf(" %d",a[j]);
            }
            return ;
        }
        if(equal(a,a+n,b))
            key=1;
        if(i>n)
            break;
    }
}

int main() {
	scanf("%d",&n);
	int a1[100],a2[100],b[100];
	for(int i=0;i<n;i++){
        scanf("%d",&a1[i]);
        a2[i]=a1[i];
	}
	for(int i=0;i<n;i++){
        scanf("%d",&b[i]);
	}
	insort(a2,b);
	mesort(a1,b);
	return 0;
}
```
