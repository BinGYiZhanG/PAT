### 思考点：
* ```place[N].price=0;place[N].distance=D;///注意```,
* ```if(priceMin<place[now].price)///注意    break;```
          
          



```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;


struct Place{
    double price;
    double distance;
}place[510];

bool cmp(const Place &a ,const Place &b){
    return a.distance<b.distance;
}

int main(){
    double Cmax;///油箱最大容量
    double D;///杭州与目的地距离
    double Davg;///没升汽油可以跑多远
    int N;///加油站数量
    cin>>Cmax>>D>>Davg>>N;
    //scanf("%lf%lf%lf%d",&Cmax,&D,&Davg,&N);
    for(int i=0;i<N;i++){
        cin>>place[i].price>>place[i].distance;
    }
    place[N].price=0;
    place[N].distance=D;///注意

    sort(place,place+N,cmp);

    if(place[0].distance!=0){
        printf("The maximum travel distance = 0\n");
    }
    else{
        int now=0;
        double ans=0,MAX=Cmax*Davg,nowTank=0;
        while(now<N){
            int k=-1,priceMin=100000000;
            for(int i=now+1;place[i].distance-place[now].distance<=MAX;i++){
                if(place[i].price<priceMin){
                    k=i;
                    priceMin=place[i].price;
                }
                if(priceMin<place[now].price)///注意
                    break;
            }
            if(k==-1)
                break;
            double need=(place[k].distance-place[now].distance)/Davg;
            if(priceMin<place[now].price){///如果当前油站的价格高于下一个油站的价格
                if(nowTank<need){
                    ans+=(need-nowTank)*place[now].price;
                    nowTank=0;
                }
                else{
                    nowTank-=need;
                }
            }
            else{
                ans+=(Cmax-nowTank)*place[now].price;
                nowTank=Cmax-need;
            }
            now=k;
        }
        if(now<N)
            printf("The maximum travel distance = %.2f\n",place[now].distance+MAX);
        else
            printf("%.2f\n",ans);
    }

}

```
