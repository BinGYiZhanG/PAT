#### 坑点：scanf无法同时读入double型，和int型，要同时读的话要用cin
#### 坑点代码:
```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxn=1000+10;

double a[maxn]={0};

int main(){
    int k;
  //  memset(a,a+maxn,0.0);
    scanf("%d",&k);
    for(int i=0;i<k;i++){
        double exp,coe;
        scanf("%lf%lf",&exp,&coe);
        a[int(exp)]=coe;
        printf("%lf %lf\n",&exp,&coe);
    }
    scanf("%d",&k);
    for(int i=0;i<k;i++){
        double exp,coe;
        scanf("%lf%lf",&exp,&coe);
        a[int(exp)]+=coe;
    }
    for (int i = 0; i < maxn; i++) {
		if (a[i] != 0){
            printf("%d %lf\n",i,a[i]);
		}
	}

    /*
    int cnt = 0;
	for (int i = 0; i < maxn; i++) {
		if (a[i] != 0)
			cnt++;
	}
	if (cnt != 0)
		printf("%d ", cnt);
	else
		printf("0");
	for (int i = maxn; i >= 0; i--) {
		if (a[i] != 0) {
			printf("%d %.1lf", i, a[i]);
			cnt--;
			if (cnt != 0) {
				printf(" ");
			}
		}

	}
	*/
}
```
坑点：scanf无法同时读入double型，和int型，要同时读的话要用cin



