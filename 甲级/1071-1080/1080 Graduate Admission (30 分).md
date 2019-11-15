* GE:高考分数，GI：面试分数，最终分数：（GE+GI）/2;
* 根据最终分数进行排名，录取也是根据最终名单，
* 如果final grade相同，则根据GE排名，如果GE相同，则他们排名相同
* 每个考生有K个录取选择，如果按照排名，这个人报了这个学校，并且该学校录取人数还未满，则录取，按照该学生的报名顺序进行录取
* 如果有相同的排名，并且包括相同的学校，即使学校已满，也可以录取

### 输入：
* N，总报考人数；M，总共的大学；K，每个申请者的可能选择个数；
#### 下一行，
* 第i个代表每个大学的人数配额，
* 接下来N行，每一行包含K+2个整数，
* GE GI K个报考学校
* 申请者的序号是0~N-1


### 输出：
* 按升序输出，如果第i号考生没被录取，输出空行
* 输出该申请者的所有可能录取的大学结果，


### 问题：
* 在排序之后，数组中单个元素的位置发生了改变，序号也随之而变，所以序号得重新定义```id```

```cpp

#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <vector>

using namespace std;

int N,M,K;
//int schools[110];///每个大学的人数配额
vector<int> ressch[110];///每个学校的录取结果

struct school{
    int quota;
    int factnum;
    int lastAdmit;
}sch[110];

struct student{
    int GE,GI;
    int FG,r;
    int perfer[5];
}stu[40010];

bool cmp(const student a,const student b){
    if(a.FG!=b.FG)
        return a.FG>b.FG;
    else
        return a.GE>b.GE;
}

bool cmpID(int a,int b){
    return a<b;
}

int main(){
    scanf("%d%d%d",&N,&M,&K);
    for(int i=0;i<M;i++){
        //scanf("%d",schools+i);
        scanf("%d",&sch[i].quota);
        sch[i].factnum=sch[i].quota;
        sch[i].lastAdmit=-1;
    }
    for(int i=0;i<N;i++){
        scanf("%d%d",&stu[i].GE,&stu[i].GI);
        stu[i].FG=(stu[i].GE+stu[i].GI);///最终分数用了int型
        for(int j=0;j<K;j++){
            scanf("%d",&stu[i].perfer[j]);
        }
    }
    sort(stu,stu+N,cmp);

    for(int i=0;i<N;i++){
        if(i>0&&stu[i].FG==stu[i-1].FG&&stu[i].GE==stu[i-1].GE){
            stu[i].r=stu[i-1].r;
        }
        else{
            stu[i].r=i;
        }
    }
    /*
    for(int i=0;i<N;i++){
        for(int k=0;k<K;k++){///报考院校搜索
            int tmp=stu[i].perfer[k];
            if(schools[tmp]>0){
                ressch[tmp].push_back(i);///插入该学生的序号
                schools[tmp]--;
                break;
            }
        }
    }
*/
    for(int i=0;i<N;i++){
        for(int k=0;k<K;k++){
            int choice=stu[i].perfer[k];
            int num=sch[choice].factnum;
            int last=sch[choice].lastAdmit;
            if(num>0||(last!=-1&&stu[i].r==stu[last].r)){
                ressch[choice].push_back(i);
                sch[choice].lastAdmit=i;
                sch[choice].factnum--;
                break;
            }
        }
    }

    for(int i=0;i<M;i++){
        int len=ressch[i].size();
        if(len==0){
            printf("\n");
        }
        else{
            sort(ressch[i].begin(),ressch[i].end(),cmpID);
            for(int j=0;j<len;j++){
                if(j==0){
                    printf("%d",ressch[i][j]);
                }
                else{
                    printf(" %d",ressch[i][j]);
                }
            }
            printf("\n");
        }
    }
    return 0;
}


```


* 26分代码

```
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <vector>

using namespace std;

int N,M,K;
//int schools[110];///每个大学的人数配额
vector<int> ressch[110];///每个学校的录取结果

struct school{
    int quota;          ///该大学招生数量
    int factnum;        ///该大学实际招生数量
    int lastAdmit;      ///该大学最后招的这位学生
}sch[110];

struct student{
    int id;
    int GE,GI;///
    int FG,r;///最后总分，排名
    int perfer[5];///该同学报考的大学
}stu[40010];

bool cmp(const student a,const student b){///按照FG排序；如果FG相同，根据GE排序
    if(a.FG!=b.FG)
        return a.FG>b.FG;
    else
        return a.GE>b.GE;
}

bool cmpID(int a,int b){
    return a<b;
}

int main(){
    scanf("%d%d%d",&N,&M,&K);///N:总报考人数 ,M:大学数量,K:每个申请者的可能选择个数；
    for(int i=0;i<M;i++){
        //scanf("%d",schools+i);
        scanf("%d",&sch[i].quota);
        sch[i].factnum=sch[i].quota;///每个大学的招生数量
        sch[i].lastAdmit=-1;
    }
    for(int i=0;i<N;i++){///初始化每个学生的GE，GI，FG成绩,和报考大学编号
        scanf("%d%d",&stu[i].GE,&stu[i].GI);
        stu[i].id=i;
        stu[i].FG=(stu[i].GE+stu[i].GI);///最终分数用了int型
        for(int j=0;j<K;j++){
            scanf("%d",&stu[i].perfer[j]);
        }
    }
    sort(stu,stu+N,cmp);///

/*
    for(int i=0;i<N;i++){///划分学生名次
        if(i>0&&stu[i].FG==stu[i-1].FG&&stu[i].GE==stu[i-1].GE){
            stu[i].r=stu[i-1].r;
        }
        else{
            stu[i].r=i;
        }
    }

    for(int i=0;i<N;i++){
        printf("id:%d r:%d \n",stu[i].id,stu[i].r);
    }

    for(int i=0;i<N;i++){
        for(int k=0;k<K;k++){///报考院校搜索
            int tmp=stu[i].perfer[k];
            if(schools[tmp]>0){
                ressch[tmp].push_back(i);///插入该学生的序号
                schools[tmp]--;
                break;
            }
        }
    }
*/
    for(int i=0;i<N;i++){
        for(int k=0;k<K;k++){
            int choice=stu[i].perfer[k];    ///学生选择的报考学校
            int num=sch[choice].factnum;    ///该学校实际招生数（应该大于0才可以继续招生）
            int last=sch[choice].lastAdmit;     //该学校最后录取的学生编号
            if(num>0||(stu[i].FG==stu[last].FG&&stu[i].GE==stu[last].GE)){///如果该学校没招满  ||  该生与前一个录取的学生的排名相同 ，则录取
                ressch[choice].push_back(stu[i].id);        ///
                sch[choice].lastAdmit=stu[i].id;
                sch[choice].factnum--;
                break;              ///只能被一个大学录取
            }
        }
    }

    for(int i=0;i<M;i++){
        int len=ressch[i].size();
        if(len==0){
            printf("\n");
        }
        else{
            sort(ressch[i].begin(),ressch[i].end(),cmpID);
            for(int j=0;j<len;j++){
                if(j==0){
                    printf("%d",ressch[i][j]);
                }
                else{
                    printf(" %d",ressch[i][j]);
                }
            }
            printf("\n");
        }
    }

    return 0;
}

```

