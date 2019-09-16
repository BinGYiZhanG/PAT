* 作为公司的总经理，你必须仔细考虑，
  * 对于每一个项目，完成它的时间，截止日期，你能获得的最大效益
* 为了决定你的小组是否参与这个项目，例如有如下3个项目：
  * ```Project[1]```花费3天时间，它一定在3天之前完成，获得6单位的利润
  * ```Project[2]```花费2天时间，它一定在3天之前完成，获得3单位的利润
  * ```Project[3]```花费3天时间，它一定在3天之前完成，获得4单位的利润

* 你或许可以参与```Project[1]```来获得6单位利润，
* 但是如果你参与```Project[2]```，你还会有一天的时间完成```Project[3]```，因此总共可以获得7单位利润

* 需要指出：如果你的小组参与一个项目，那么就得从头到尾没有打断的参与该项目

### 输入：

* 第一行，N，代表接下来的N行项目，
* 接下来N行，每行包含3个数字：P，该项目利润；L，该项目的持续时间；D，该项目的截止日期
* 保证L绝不大于D，所有数字为非负整数

### 输出：

* 输出你能得到的最大利润


[题解](https://www.cnblogs.com/zsyacm666666/p/6936625.html)

* 设dp[i][j]表示考虑到第i个项目，前一个项目结束时间为j的最大收益,那么可得DP方程为:
* dp[i][j+a[i].l]=max(dp[i][j+a[i].l],dp[k][j]) if(j+a[i].l<=a[i].d)
* 由于没有说明数据范围，只能使用map表示二维dp数组了

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <map>

using namespace std;

typedef long long ll;

const int maxn=1e5+10;
const int inf=0x3f3f3f3f;

map<ll,map<ll,ll> > dp;
int n;

struct Project{
    int p;///最大效益
    int l;///持续时间
    int d;///截止日期

    bool operator <(const Project &p)const {
        return d<p.d;
    }
}proj[55];

/*
int main(){
    while(scanf("%d",&n)!=EOF){
        for(int i=0;i<55;i++)
            mp[i].clear();

        ll ans=0;
        mp[0][0]=0;
        for(int i=0;i<n;i++)
            cin>>proj[i].p>>proj[i].l>>proj[i].d;

        sort(proj,proj+n);

        for(int i=0;i<n;i++){
            mp[i+1]=mp[i];

            for(it=mp[i].begin();it!=mp[i].end();it++)
                if(it->first+proj[i].l<=proj[i].d)///如果该任务在时间允许范围内
                    ans=max(ans,mp[i+1][it->first+proj[i].l=max(mp[i+1][it->first+proj[i].l],it->second+proj[i].p));
        }           ///
    }
}

*/

int main(){
    while(scanf("%d",&n)!=EOF){
        for(int i=1;i<=n;i++)
            scanf("%d%d%d",&proj[i].p,&proj[i].l,&proj[i].d);

        proj[0].d=proj[0].l=proj[0].p=0;

        sort(proj+1,proj+n+1);

        dp.clear();

        ll ans=0;

        for(int i=1;i<=n;i++)
            for(int j=0;j<=proj[i-1].d;j++)
            if(j+proj[i].l<=proj[i].d)///在第i-1个项目截止日期之前，更新插入第i个项目
                for(int k=0;k<i;k++){///遍历前i个项目
                    dp[i][j+proj[i].l]=max(dp[i][j+proj[i].l],dp[k][j]+proj[i].p);
                ///完成第i个项目，时间为j+proj[i].l，的最大收益为：
                ///完成前k个项目，完成时间为j的收益加上，第i个项目的收益   与    完成第i个项目，时间为j+proj[i].l  的收益   的最大值
                    ans=max(ans,dp[i][j+proj[i].l]);
                }

        cout<<ans<<endl;
    }
}
```



