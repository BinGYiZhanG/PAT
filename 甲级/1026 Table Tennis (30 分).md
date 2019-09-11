一个桌球俱乐部有N张桌子提供给大众。球桌的编号是1~N。对于任何球员来说，当他们到达时如果有一些球桌是空闲的，他们将会被分配到空闲最小编号球桌。<br>
如果所有球桌都被占据，他们将进入一个等待队列。假定每位球员最多玩2个小时。<br>

你的工作是计数在队列中的每个人的等待时间，并且对于对于每张球桌在该天的服务球员数。<br>

有一件事使得过程变得有点复杂，是俱乐部会预留一些桌子给它的VIP会员。当一个VIP球桌空闲时，在队列里的第一个VIP球员将会有特权使用它。然而，如果没有VIP球员在队列的话，下一个球员将会使用它。另一方面，如果轮到VIP球员，但是没有VIP球桌，球桌会分配给任何球员。<br>


### 输入：
第一行，N，球员总数；<br>
接下来N行，将包含两个时间，和一个VIP标志：<br>
```HH:MM:SS``` 到达时间；```P```球员玩耍时间；```tag```如果是VIP，置1,；不是VIP置0。<br>
保证当俱乐部开着的时候，到达时间在```08:00:00```到```10:00:00```之间。保证没有两个顾客的到达时间相同。<br>
接下来是球员信息，K，球桌数；M，VIP球桌数。<br>
最后一行，M个球桌编号.<br>

### 输出：
对于每个测试用例，首先打印```the arriving time```，```serving time```和对于每一个球员如示例所示的等待时间。<br>
然后在一行上打印每个球桌服务的球员数。<br>
注意输出应该按服务时间的周期顺序列出。等待时间应该是一个向上取整的分钟。如果在关闭时间之前一个人没有得到一张桌子，他的时间信息将不会被打印。<br>

### Sample Input
```
9
20:52:00 10 0
08:00:00 20 0
08:02:00 30 0
20:51:00 10 0
08:10:00 5 0
08:12:00 10 1
20:50:00 10 0
08:01:30 15 1
20:53:00 10 1
3 1
2
```
### Sample Output
```
08:00:00 08:00:00 0
08:01:30 08:01:30 0
08:02:00 08:02:00 0
08:12:00 08:16:30 5
08:10:00 08:20:00 10
20:50:00 20:50:00 0
20:51:00 20:51:00 0
20:52:00 20:52:00 0
3 3 2
```


```cpp
#include <iostream>
#include <cstdio>
#include <cmath>
#include <algorithm>
#include <vector>

using namespace std;

const int K=111;            ///窗口数
const int inf=0x3f3f3f3f;           ///无穷大

struct Player{
    int arrTime,stTime,trTime;///到达时间，训练开始时间及训练时长
    bool isVIP;             ///是否是VIP球员
}newPlayer;                 ///临时存放新读入的球员

struct Table{
    int endTime,numServe;     ///当前占用该球桌的球员的结束时间及已训练的人数
    bool isVIP;             ///是否是VIP球桌
}table[K];                  ///K个球桌

vector<Player> player;      ///球员队列

int convertTime(int h,int m,int s){
    return h*3600+m*60+s;
}

///按到达时间排序
bool cmpArrTime(const Player& a,const Player& b){
    return a.arrTime<b.arrTime;
}

///按开始时间排序
bool cmpStTime(const Player& a,const Player& b){
    return a.stTime<b.stTime;
}

///编号VIPi从当前VIP球员移到下一个VIP球员
int nextVIPPlayer(int VIPi){
    VIPi++;                     ///先将VIPi加1
    while(VIPi<(int)player.size()&&player[VIPi].isVIP==0)
        VIPi++;
    return VIPi;            ///返回下一个VIP球员的ID
}

///将编号为tID的球桌分配给编号为pID的球员
void allotTable(int pID,int tID){
    if(player[pID].arrTime<=table[tID].endTime) ///更新球员的开始时间
        player[pID].stTime=table[tID].endTime;
    else
        player[pID].stTime=player[pID].arrTime;

    ///该球桌的训练结束时间更新为新球员的结束时间，并让服务人数加1
    table[tID].endTime=player[pID].stTime+player[pID].trTime;
    table[tID].numServe++;

}

int main(){
    int n,k,m,VIPtable;
    scanf("%d",&n);         ///球员数
    int stTime=convertTime(8,0,0);          ///开门时间为8点
    int edTime=convertTime(21,0,0);         ///关门时间为21点

    for(int i=0;i<n;i++){
        int h,m,s,trainTime,isVIP;///时，分，秒，训练时长，是否为VIP球员
        scanf("%d:%d:%d %d %d",&h,&m,&s,&trainTime,&isVIP);
        newPlayer.arrTime=convertTime(h,m,s);           ///到达时间
        newPlayer.stTime=edTime;                        ///开始时间初始化为21点
        if(newPlayer.arrTime>=edTime)
            continue;                   ///21点以后的直接排除

        ///训练时长
        newPlayer.trTime=trainTime<=120?trainTime*60:7200;
        newPlayer.isVIP=isVIP;              ///是否是VIP
        player.push_back(newPlayer);        ///将newPlayer加入到球员队列中
    }

    scanf("%d%d",&k,&m);            ///球桌数，VIP球桌数

    for(int i=1;i<=k;i++){
        table[i].endTime=stTime;        ///当前训练结束时间为8点
        table[i].numServe=table[i].isVIP=0;///  初始化numServe和isVIP
    }

    for(int i=0;i<m;i++){
        scanf("%d",&VIPtable);              ///VIP球桌编号
        table[VIPtable].isVIP=1;            ///记为VIP球桌
    }

    sort(player.begin(),player.end(),cmpArrTime);
    int i=0,VIPi=-1;            ///i用来扫描所有球员，VIPi总是指向当前最前的VIP球员

    VIPi=nextVIPPlayer(VIPi);       ///找到第一个VIP球员的编号

    while(i<(int)player.size()){         ///当前队列最前面的球员为i
        int idx=-1,minEndTime=inf;      ///寻找最早能空闲的球桌
        for(int j=1;j<=k;j++){
            if(table[j].endTime<minEndTime){
                minEndTime=table[j].endTime;
                idx=j;
            }
        }

        ///idx为最早空闲的球桌编号
        if(table[idx].endTime>=edTime)
            break;      ///已经关门，直接break

        if(player[i].isVIP==1&&i<VIPi){
            i++;
            continue;
        }

        ///以下按球桌是否为VIP，球员是否为VIP，进行4中情况的讨论
        if(table[idx].isVIP==1){
            if(player[i].isVIP==1){///1，球桌是VIP，球员是VIP
                allotTable(i,idx);///将球桌idx分配给球员i
                if(VIPi==i)
                    VIPi=nextVIPPlayer(VIPi);///找到下一个VIP球员
                i++;///i号球员开始训练，因此继续队列的下一个人
            }else{      ///2，如果球桌是VIP，球员不是VIP
            ///如果当前队首的VIP球员比该VIP球桌早，就把球桌idx分配给他
                if(VIPi<(int)player.size()&&player[VIPi].arrTime<=table[idx].endTime){
                    allotTable(VIPi,idx);           ///将球桌idx分配给球员VIPi
                    VIPi=nextVIPPlayer(VIPi);       ///找到下一个VIP球员
                }
                else{
                ///队首VIP球员比该VIP球桌迟，仍然把球桌idx分配给球员i
                    allotTable(i,idx);      ///将球桌idx分配给球员i
                    i++;        ///i号球员开始训练，因此继续队列的下一个人
                }
            }
        }
        else{
            if(player[i].isVIP==0){///3，球桌不是VIP，球员不是VIP
                allotTable(i,idx);///将球桌idx分配给球员i
                i++;            ///i号球员开始训练，因此继续队列的下一个人
            }else{          ///4，球桌不是VIP，球员是VIP
                ///找到最早空闲的VIP球桌
                int VIPidx=-1,minVIPEndTime=inf;
                for(int j=1;j<=k;j++){
                    if(table[j].isVIP==1&&table[j].endTime<minVIPEndTime){
                        minVIPEndTime=table[j].endTime;
                        VIPidx=j;
                    }
                }

                ///最早空闲的VIP球桌编号是VIPidx
                if(VIPidx!=-1&&player[i].arrTime>=table[VIPidx].endTime){
                    ///如果VIP球桌存在，且空闲时间比球员来的时间早
                    ///就把它分配给球员i
                    allotTable(i,VIPidx);
                    if(VIPi==i)
                        VIPi=nextVIPPlayer(VIPi);///找到下一个VIP球员
                    i++;///i号球员开始训练，因此继续队列的下一个人
                }
                else{
                    ///如果球员来时VIP球桌还未空闲，就把球桌idx分配给他
                    allotTable(i,idx);
                    if(VIPi==i)
                        VIPi=nextVIPPlayer(VIPi);           ///找到下一个VIP球员
                        i++;        ///i号球员开始训练，因此继续队列的下一个人
                }
            }
        }
    }

    sort(player.begin(),player.end(),cmpStTime);///按开始时间排序
    for(i=0;i<(int)player.size()&&player[i].stTime<edTime;i++){
        int t1=player[i].arrTime;
        int t2=player[i].stTime;
        printf("%02d:%02d:%02d ",t1/3600,t1%3600/60,t1%60);
        printf("%02d:%02d:%02d ",t2/3600,t2%3600/60,t2%60);
        printf("%.0f\n",round((t2-t1)/60.0));
    }

    for(i=1;i<=k;i++){
        printf("%d",table[i].numServe);
        if(i<k)
            printf(" ");
    }
    return 0;
}


```












