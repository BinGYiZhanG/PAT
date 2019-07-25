福布斯杂志每年都会发布一个亿万富翁排行榜基于每年全世界最富有的人的排名。现在你应该模仿这份工作，但是只聚焦于特定年龄范围的人们。<br>
也就是说，给出N个人的净财富，你应该在被给年龄范围找到M个最富有的人。<br>

### 输入：
第一行，N($<\leq 10^{5}$)，总人数；K($<\leq 10^{3}$),查询个数。
接下来N行，每行包含姓名（不超过8个字符，不带空格），age（在[0,200]的整数）,the net worth ($[-10^{6},10^{6}]$)。<br>
最后给出K行查询，每行包含3个正数：M($\leq100$),输出的最大数，和年龄范围```[Amin,Amax]```。<br>

### 输出：
在每一行，首先打印```Case #X```,X是查询数字从1开始，输出年龄范围[Amin,Amax]的M个最富有的人。每个人的信息的格式：<br>
```
Name Age Net_Worth
```

输出是the net worths的递减序。如果存在相等的worths，则按age的递增序排列，如果worths与age都一样，输出按照名字的字母序排列。<br>
保证没有两个人有三个相同的信息。如果没有人被发现，输出“None”。


### 测试点2出错
格式问题,
![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07250953.png)
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <vector>

using namespace std;

int N,K;
struct node{
    char name[10];
    int age,worth;
}per[100010];
int book[110];///记录是否超范围，因为M最大是100，所以设110

bool cmp(node a,node b){
    if(a.worth!=b.worth)
        return a.worth>b.worth;
    else if(a.age!=b.age)
        return a.age<b.age;
    else
        return (strcmp(a.name,b.name)<0);///字母序是前面那个小，-1
}

int main(){
    vector<node> vec;
    scanf("%d%d",&N,&K);
    for(int i=0;i<N;i++){
        scanf("%s %d %d",per[i].name,&per[i].age,&per[i].worth);
        if(book[per[i].age]<100){
            vec.push_back(per[i]);
            book[per[i].age]++;
        }
    }
    sort(vec.begin(),vec.end(),cmp);
    int amin,amax,M;
    for(int i=1;i<=K;i++){
        scanf("%d%d%d",&M,&amin,&amax);

        printf("Case #%d:\n",i);
        vector<node> t;
		for (int j = 0; j < (int)vec.size(); j++) {
			if (vec[j].age >= amin && vec[j].age <= amax) {
				t.push_back(vec[j]);
			}
		}
		int flag = 0;
		for (int j = 0; j < M&&j < (int)t.size(); j++) {
			printf("%s %d %d\n", t[j].name, t[j].age, t[j].worth);
			flag = 1;
		}
		if (flag == 0)
			printf("None\n");

    }

}
```
