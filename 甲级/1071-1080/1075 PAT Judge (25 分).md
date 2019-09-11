### 题意：

#### 输入：
* $N（）$，用户总数；K，问题总数；M，提交总数，
* 用户的id从00001到N，问题的id从1到K
* 接下来一行包含K个正整数p[i],对应于每个题目的满分值
* 接下来M行，给出如下格式的信息：
  * ```用户id 问题id 该题得分值```
  * 如果```该题得分值```是-1，相当于提交未通过编译器，
  * 该得分值只能在[0,该题满分]之间

#### 输出：
* 以以下格式输出：
  * ```排名 用户id 总得分 s[1] ... s[K] ```
  * ```排名```基于```总得分```,如果```总得分```相同，```排名```相同
  * 如果用户对一个问题从未提交，则输出```-```，
  * 如果用户对一个问题多次提交，则记录最高分
* 排名规则：
  * 排名表以非递减序打印
  * 如果存在相同```排名```，则比较```完美解题数```
  * 如果仍然平局，按升序打印他们的```id```
  * 如果用户的提交从未通过编译器，则不会被记录在```ranklist```中，
  * 保证至少有一个用户在```ranklist```中
  
  
  
#### 存在一个问题：
如果用户不在```ranklist```中，那他会参加排名吗?

#### 我的22分代码，最后一个测试点始终过不了

```
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>
#include <vector>
using namespace std;

const int maxn = 10010;
const int maxpro = 6;

//结构体初始化
struct student {
	int id;
	int scr[maxpro];
	int tol_scr;
	int cnt ;
	int perfect_pro;
	int rank;
}stu[maxn];
int problem_full[maxpro] = { 0 };
int n, k, m;
bool cmp(student &a, student &b) {
	if (a.tol_scr != b.tol_scr)
		return a.tol_scr > b.tol_scr;
	else if (a.perfect_pro != b.perfect_pro)
		return a.perfect_pro > b.perfect_pro;
	else
		return a.id < b.id;
}

void init(){
  for(int i=1;i<=n;i++){
    stu[i].id=i;
    stu[i].tol_scr=0;
    stu[i].cnt=0;
    stu[i].perfect_pro=0;
    stu[i].rank=0;
    fill(stu[i].scr,stu[i].scr+6,-1);
  }
}

int main() {
  scanf("%d%d%d",&n,&k,&m);
	for (int i = 1; i <= k; i++) {
	  scanf("%d",&problem_full[i]);
	}
	//不用非得记录考生的id，输出时，按照格式输出即可
	init();
	for (int i = 0; i < m;i++) {
		int tmp,num,score;
		scanf("%d%d%d",&tmp,&num,&score);
		if (score == -1&& stu[tmp].scr[num]==-1) {//如果该提交为通过编译器，并且该同学提交该题的分数为-1
			stu[tmp].scr[num] = 0;///设-1是从未提交，0是提交过但是错了

		}
		else {
			if (problem_full[num] == score) {       ///提交得分为满分，完美题解数加1
				stu[tmp].perfect_pro++;
			}
			if(score>stu[tmp].scr[num]&& stu[tmp].scr[num]<problem_full[num])   //如果提交得分高于已提交分数，低于该题满分，更新该题得分
				stu[tmp].scr[num] = score;
			stu[tmp].cnt++;
		}
	}
	for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= k; j++) {
			if (stu[i].scr[j] != -1) {
				stu[i].tol_scr += stu[i].scr[j];///计算每位学生的总得分
			}
		}
	}
	sort(stu+1, stu + n+1, cmp);
	stu[1].rank = 1;
	for (int i = 2; i <= n; i++) {///计算每个人的排名
		if (stu[i].tol_scr == stu[i - 1].tol_scr) {
			stu[i].rank = stu[i - 1].rank;
		}
		else {
			stu[i].rank = i;
		}
	}

	for (int i = 1; i <= n; i++) {
		if (stu[i].cnt) {
			printf("%d %05d %d", stu[i].rank, stu[i].id, stu[i].tol_scr);
			for (int j = 1; j <= k; j++) {
				if (stu[i].scr[j] == -1)
					printf(" -");
				else
					printf(" %d", stu[i].scr[j]);
			}
			printf("\n");
		}
	}
	return 0;
}

```




#### AC代码

```
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct node{
    int rank_,id,total=0;
    vector<int> scr;
    int passnum=0;
    bool isshown=false;
};

bool cmp(const node& a,const node& b){
    if(a.total!=b.total)
        return a.total>b.total;
    else if(a.passnum!=b.passnum)
        return a.passnum>b.passnum;
    else
        return a.id<b.id;
}

int main(){
    int n,m,k,id,num,scr;
    scanf("%d%d%d",&n,&k,&m);
    vector<node> v(n+1);
    for(int i=1;i<=n;i++)
        v[i].scr.resize(k+1,-1);

    vector<int> full(k+1);

    for(int i=1;i<=k;i++)
        scanf("%d",&full[i]);

    for(int i=0;i<m;i++){
        scanf("%d%d%d",&id,&num,&scr);
        v[id].id=id;
        v[id].scr[num]=max(v[id].scr[num],scr);
        if(scr!=-1)
            v[id].isshown=true;
        else if(v[id].scr[num]==-1)
            v[id].scr[num]=-2;
    }

    for(int i=1;i<=n;i++){
        for(int j=1;j<=k;j++){
            if(v[i].scr[j]!=-1&&v[i].scr[j]!=-2)
                v[i].total+=v[i].scr[j];
            if(v[i].scr[j]==full[j])
                v[i].passnum++;
        }
    }

    sort(v.begin()+1,v.end(),cmp);

    for(int i=1;i<=n;i++){
        v[i].rank_=i;
        if(i!=1&&v[i].total==v[i-1].total)
            v[i].rank_=v[i-1].rank_;
    }

    for(int i=1;i<=n;i++){
        if(v[i].isshown==true){
            printf("%d %05d %d",v[i].rank_,v[i].id,v[i].total);
            for(int j=1;j<=k;j++){
                if(v[i].scr[j]!=-1&&v[i].scr[j]!=-2)
                    printf(" %d",v[i].scr[j]);
                else if(v[i].scr[j]==-1)
                    printf(" -");
                else
                    printf(" 0");
            }
            cout<<endl;
        }
    }
}


```
