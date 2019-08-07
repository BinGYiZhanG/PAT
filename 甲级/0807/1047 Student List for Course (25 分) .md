超时代码21分
```cpp
#include <cstdio>
#include <iostream>
#include <cstring>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

vector<string> vec[2550];

bool cmp(string a,string b){
    return a<b;
}

int main(){
    int n,k;
    scanf("%d%d",&n,&k);
    for(int i=0;i<n;i++){
        int num;
        string str;
        cin>>str>>num;
        for(int j=0;j<num;j++){
            int tmp;
            cin>>tmp;
            vec[tmp].push_back(str);
        }
    }

    for(int i=1;i<=k;i++){
        int len=vec[i].size();
        printf("%d %d\n",i,len);
        sort(vec[i].begin(),vec[i].end(),cmp);
        for(int j=0;j<len;j++){
            cout<<vec[i][j]<<endl;
        }
    }
}
```


AC代码:
```cpp
#include <cstdio>
#include <cstring>
#include <vector>
#include <algorithm>
using namespace std;
const int maxn=40010;       //最大学生人数
const int maxc=2510;        //最大课程人数

char name[maxn][5];//maxn个学生
vector<int> course[maxc];//course[i]存放第i门课的所有学生编号

bool cmp(int a,int b){
    return strcmp(name[a],name[b])<0;//按姓名字典序从小到大排序
}

int main(){
    int N,K,c,courseID;
    scanf("%d%d",&N,&K);
    for(int i=0;i<N;i++){
        scanf("%s%d",name[i],&c);
        for(int j=0;j<c;j++){
            scanf("%d",&courseID);
            course[courseID].push_back(i);
        }
    }
    for(int i=1;i<=K;i++){
    //为什么i的区间是[1,K],而不是[0,K-1].
    //因为读入选择的课程编号，他们的编号就是从1开始的
        printf("%d %d\n",i,course[i].size());
        sort(course[i].begin(),course[i].end(),cmp);
        for(int j=0;j<course[i].size();j++){
            printf("%s\n",name[course[i][j]]);
        }
    }
    return 0;
}
```
