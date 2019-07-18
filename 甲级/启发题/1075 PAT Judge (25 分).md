PAT排名从状态表中产生，展示了提交分数。这次你应该生成一个PAT排名表。<br>
输入：
N，用户的总数；K，问题总数；M，提交总数。假定用户的id从00001到N，问题序号从1~K，它包含K个正数，
K个正数，
```用户序号 问题序号 得分```
得分在-1，[0, p[problem_id]]

输出：
```排名 用户序号 总分 每个题的得分```
未提交显示'-',
最高分记录
排序顺序:完美解题数，id号，
如果用户一个题都没解出来，不能显示在排名里。

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

const int maxn=10010;
const int maxpro=6;

struct student{
    int id;
    int scr[maxpro];
    int tol_scr;
    int cnt;
    int per_pro;
    int rank_;
}stu[maxn];

int pro_full[maxpro]={0};
int n,k,m;
bool cmp(student &a,student &b){
    if(a.tol_scr!=b.tol_scr)
        return a.tol_scr>b.tol_scr;
    else if(a.per_pro!=b.per_pro)
        return a.per_pro>b.per_pro;
    else
        return a.id<b.id;
}

void init(){
    for(int i=1;i<=n;i++){
        stu[i].id=i;
        stu[i].tol_scr=0;
        stu[i].cnt=0;
        stu[i].per_pro=0;
        stu[i].rank_=0;
        fill(stu[i].scr,stu[i].scr+6,-1);
    }
}

int main(){
    scanf("%d%d%d",&n,&k,&m);
    for(int i=1;i<=k;i++){
        scanf("%d",&pro_full[i]);
    }
    init();
    for(int i=0;i<m;i++){
        int tmp,num,Scr;
        scanf("%d%d%d",&tmp,&num,&Scr);
        ///提交过
        if(Scr==-1&&stu[tmp].scr[num]==-1){
            stu[tmp].scr[num]=0;
        }
        else{
            if(pro_full[num]==Scr)
                stu[tmp].per_pro++;
            if(Scr>stu[tmp].scr[num]&&stu[tmp].scr[num]<pro_full[num])
                stu[tmp].scr[num]=Scr;
            stu[tmp].cnt++;///记录是否解过题
        }
    }
    for(int i=1;i<=n;i++){
        for(int j=1;j<=k;j++){
            if(stu[i].scr[j]!=-1)
                stu[i].tol_scr+=stu[i].scr[j];
        }
    }

    sort(stu+1,stu+n+1,cmp);
    stu[1].rank_=1;
    for(int i=2;i<=n;i++){
        if(stu[i].tol_scr==stu[i-1].tol_scr)
            stu[i].rank_=stu[i-1].rank_;
        else
            stu[i].rank_=i;
    }

    for(int i=1;i<=n;i++){
        if(stu[i].cnt){
            printf("%d %05d %d",stu[i].rank_,stu[i].id,stu[i].tol_scr);
            for(int j=1;j<=k;j++){
                if(stu[i].scr[j]==-1)
                    printf(" -");
                else
                    printf(" %d",stu[i].scr[j]);
            }
            printf("\n");
        }
    }
    return 0;
}


```
