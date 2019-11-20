### 题意：
* 寻找在校园内停留时间最长的车牌号，和最大停留时间，

### 输出：
* 校园内停留时间最长的车牌号，和最大停留时间，

### 思路：
* 直接模拟，单独开辟一个```Car```数组，记录合法（满足题意）的车辆信息


```
#include<iostream>
#include<cstdio>
#include<cstring>
#include<map>
#include<algorithm>
using namespace std;
const int maxn = 10010;
struct Car {
    char id[8];
    int time;
    char status[4];
}all[maxn], valid[maxn];
int num = 0;
map<string, int> parkTime;
int timeToint(int hh, int mm, int ss) {//时间转换函数,
    return hh * 3600 + mm * 60 + ss;
}
bool cmpByIdandTime(Car a, Car b) {
    if(strcmp(a.id, b.id)) {
        return strcmp(a.id, b.id) < 0;
    } else {
        return a.time < b.time;
    }
}
bool cmpByTime(Car a, Car b) {
    return a.time < b.time;
}
int main() {
    int n, k, hh, mm, ss;
    scanf("%d%d", &n, &k);
    for(int i = 0; i < n; i++) {
        scanf("%s %d:%d:%d %s", all[i].id, &hh, &mm, &ss, all[i].status);
        all[i].time = timeToint(hh, mm, ss);
    }
    sort(all, all + n, cmpByIdandTime);
    int maxTime = -1;
    for(int i = 0; i < n - 1; i++) {
        if(!strcmp(all[i].id, all[i+1].id) && !strcmp(all[i].status, "in") && !strcmp(all[i + 1].status, "out")) {
        ///对车辆进行筛选，只有上一辆的status是in,下一辆的status是out,才能使valid的
            valid[num++] = all[i];
            valid[num++] = all[i + 1];
            int inTime = all[i + 1].time - all[i].time;//记录车辆的停留时间
            if(parkTime.count(all[i].id) == 0) {//如果停车号中没有这个这个号，就开辟一个键，进行记录
                parkTime[all[i].id] = 0;
            }
            parkTime[all[i].id] += inTime;///记录该车牌号的总停留时间
            maxTime = max(maxTime, parkTime[all[i].id]);///取最大车牌号中最大停留时间
        }
    }
    sort(valid, valid + num, cmpByTime);
    int now = 0, numCar = 0;
    for(int i = 0; i < k; i++) {
        scanf("%d:%d:%d", &hh, &mm, &ss);
        int time = timeToint(hh, mm, ss);
        while(now < num && valid[now].time <= time) {///记录该时间范围内，校园内有多少辆车
            if(!strcmp(valid[now].status, "in")) {///in进来,numCar++
                numCar++;
            } else {//out出去,numCar--
                numCar--;
            }
            now++;
        }
        printf("%d\n",numCar);
    }
    map<string, int>::iterator it;
    for(it = parkTime.begin(); it != parkTime.end(); it++) {
        if(it->second == maxTime) {///输出停留最大时间的车牌号
            printf("%s ", it->first.c_str());
        }
    }
    printf("%02d:%02d:%02d\n",maxTime / 3600, maxTime % 3600 / 60, maxTime % 60);
    return 0;
}


```
