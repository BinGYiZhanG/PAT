### 题意：

### 输入：
* 第一行是给出一个正数N
* 接下来N行，每行给出个人的信息，以如下格式：
  * ```ID Father Mother k Child1 ... Childk Mestate  Area```
* ```ID```是一个4位数的身份标识，
  * ```Father```和```Mother```是该ID的父母，如果父母过世，则用```-1```代替
  * ```k```(0 \leq k \leq 5)  是这个人孩子的数目，```Childi`s```是这个孩子的```ID```,
  * ```Mestate```是在他/她名下的真实房产数目，```Area```是他/她的房产的总面积
### 输出
* 第一行，输出家庭总数
* 第二行往后输出，家庭信息，以如下格式:
  * ``` ID M AVGsets AVGarea ```
  * ```ID```是这个家庭的最小```ID```,```M```是家庭总成员数,
  * ```AVGsets  ```,他们房地产的平均数目,```AVGarea```是平均面积
  * 平均值最多精确为小数点后3位，
  * 按照平均面积的降序，ID的升序对家庭信息进行排序
  

```
#include <bits/stdc++.h>

using namespace std;

/*
id:
fid:父节点ID
mid:母亲结点ID
num:房产数
area:房产面积
cid[]:孩子结点ID
*/

struct Data{
    int id,fid,mid,num,area;
    int cid[10];
}data[1005];

/*
id:家庭最小ID,
people:家庭的人数
num:家庭的平均房产数
area:家庭的平均房产面积
flag:记录家庭数,
*/
struct node{
    int id,people;
    double num,area;
    bool flag=false;
}ans[10000];

int father[10000];
bool vis[10000];

int Find(int x){
    while(x!=father[x])
        x=father[x];

    return x;
}

//合并后，ID最小的作为根节点
void Union(int a,int b){
    int faA=Find(a);
    int faB=Find(b);

    if(faA>faB)
        father[faA]=faB;
    else if(faA<faB)
        father[faB]=faA;
}

bool cmp(const node &a,const node& b){
    if(a.area!=b.area)
        return a.area>b.area;
    else
        return a.id<b.id;
}

int main(){
    int n,k,cnt=0;
    scanf("%d",&n);

    for(int i=0;i<10000;i++)
        father[i]=i;

    for(int i=0;i<n;i++){
        scanf("%d %d %d %d",&data[i].id,&data[i].fid,&data[i].mid,&k);

        vis[data[i].id]=true;

        if(data[i].fid!=-1){
            vis[data[i].fid]=true;
            Union(data[i].fid,data[i].id);
        }

        if(data[i].mid!=-1){
            vis[data[i].mid]=true;
            Union(data[i].mid,data[i].id);
        }

        for(int j=0;j<k;j++){
            scanf("%d",&data[i].cid[j]);
            vis[data[i].cid[j]]=true;
            Union(data[i].cid[j],data[i].id);
        }

        scanf("%d %d",&data[i].num,&data[i].area);
    }

    for(int i=0;i<n;i++){
        int id=Find(data[i].id);
        ans[id].id=id;
        ans[id].num+=data[i].num;
        ans[id].area+=data[i].area;
        ans[id].flag=true;
    }

    for(int i=0;i<10000;i++){
        if(vis[i])//统计每个家庭人数
            ans[Find(i)].people++;
        if(ans[i].flag)//统计家庭数
            cnt++;
    }

    for(int i=0;i<10000;i++){
        if(ans[i].flag){
            ans[i].num=(double)(ans[i].num*1.0/ans[i].people);///计算平均房产数
            ans[i].area=(double)(ans[i].area*1.0/ans[i].people);///计算平均房产面积
        }
    }

    sort(ans,ans+10000,cmp);
    printf("%d\n",cnt);

    for(int i=0;i<cnt;i++)
        printf("%04d %d %.3f %.3f\n",ans[i].id,ans[i].people,ans[i].num,ans[i].area);

    return 0;
}

```
