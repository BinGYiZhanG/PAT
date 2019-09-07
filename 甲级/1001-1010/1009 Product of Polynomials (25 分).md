### 题目大意：给出两个多项式A和B，求A*B的结果～

* double型输出时要用%f,而非%lf

```cpp
#include <bits/stdc++.h>

using namespace std;

const int maxn=1005;
double a[maxn],b[maxn],c[2*maxn];

int main(){
    int k1,k2;
    int exp;
    double coe;
    scanf("%d",&k1);
    for(int i=0;i<k1;i++){
        cin>>exp>>coe;
        a[exp]=coe;
    }

    scanf("%d",&k2);
    for(int i=0;i<k2;i++){
        cin>>exp>>coe;
        b[exp]=coe;
        for(int i=0;i<maxn;i++){
            if(a[i]!=0){
                c[i+exp]+=b[exp]*a[i];
            }
        }
    }
    int cnt=0;
    for(int i=0;i<2001;i++){
        if(c[i]){
            cnt++;
        }
    }
    printf("%d",cnt);
    for(int i=2000;i>=0;i--){
        if(c[i]!=0){
            printf(" %d %.1f",i,c[i]);//double型输出时要用%f,而非%lf
            //cout<<i<<" "<<c[i]<<endl;
        }
    }
    return 0;
}

```
