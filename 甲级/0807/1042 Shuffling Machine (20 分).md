### 注意：
* 花色输出，有0号位，该如何处理
* 

洗牌是一个被用来随机化扑克牌的过程。因为标准洗牌技术看起来是孱弱的，并且为了避免“内部操作”雇员和赌徒勾结，通过产生不充分的洗牌，许多赌场使用自动洗牌机。<br>
你的任务是模拟一个自动洗牌机。<br>

机器洗54张牌根据给出的随机顺序并且重复给定的次数。假定牌的初始状态的如下顺序：
```
S1, S2, ..., S13, 
H1, H2, ..., H13, 
C1, C2, ..., C13, 
D1, D2, ..., D13, 
J1, J2
```
“S”代表“Spade”，“H”代表“Heart”，“C”代表“Club”，“D”代表“Diamond”，“J”代表“Joker”。给定的顺序是$[1,54]$区间中唯一的整数的递归。<br>
如果$i-th$的位置的数是$j$，意味着牌从位置$i$移动到位置$j$。例如，假定我们只有5张牌：```S3, H5, C1, D13 and J2.```。<br>
给定一个洗牌顺序```{4,2,5,3,1} ```，结果为```J2, H5, D13, S3, C1 ```。如果我们再次重复洗牌，结果是：```C1, H5, S3, J2, D13.```<br>


### 输入：
第一行，K，重复次数；<br>
接下来一行包含给给定的顺序。


### 输出：
打印牌面

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

char dos[]={'S','H','C','D','J'};
int nex[55],now[55],did[55];

///问题在于：如何记录花色
///1~13是S，
///14~ :H
///...
int main(){
    int K;
    scanf("%d",&K);
    for(int i=1;i<=54;i++)
        scanf("%d",&nex[i]);
    for(int i=1;i<=54;i++)
        now[i]=i;

    for(int i=1;i<=K;i++){
        for(int j=1;j<=54;j++){
            did[nex[j]]=now[j];
        }
        for(int j=1;j<=54;j++){
            now[j]=did[j];
        }
    }

    for(int i=1;i<=54;i++){
        now[i]--;//mp数组存在0号位,所以start需要--
        if(i==1)
            printf("%c%d",dos[now[i]/13],now[i]%13+1);
        else
            printf(" %c%d",dos[now[i]/13],now[i]%13+1);
    }
}

```
