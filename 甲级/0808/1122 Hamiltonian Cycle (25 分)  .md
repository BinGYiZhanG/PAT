

我的16分代码,

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

int e[210][210],n,m,k,f[210];
bool vis[210];
int nums;

void DFS(int v){
    vis[v]=true;
    for(int i=0;i<nums;i++){
        if(vis[f[i]]==false&&e[v][f[i]]){
            DFS(f[i]);
        }
    }
}

int main()
{
    int a,b;
    scanf("%d%d",&n,&m);
    for(int i=0;i<m;i++){
        scanf("%d%d",&a,&b);
        e[a][b]=e[b][a]=1;
    }
    scanf("%d",&k);
    for(int i=0;i<k;i++){
        memset(vis,0,sizeof(vis));
        scanf("%d",&nums);
        for(int j=0;j<nums;j++){
            scanf("%d",&f[j]);
        }
        if(nums!=n+1){///点不符合，直接判断不是哈密顿
            printf("NO\n");
        }
        else{
           // bool flag=true;///默认是哈密顿
            int cnt=0;
            for(int j=0;j<nums;j++){
                if(vis[f[j]]==false){
                    DFS(f[j]);
                    cnt++;
                }
            }
            if(cnt==1&&f[0]==f[nums-1])
                printf("YES\n");
            else
                printf("NO\n");
        }
    }
    return 0;
}

```



```cpp
#include <iostream>
#include <set>
#include <vector>
using namespace std;

int main() {
	int n, m, cnt, k, a[210][210] = { 0 };
	cin >> n >> m;
	for (int i = 0; i < m; i++) {
		int t1, t2;
		scanf("%d%d", &t1, &t2);
		a[t1][t2] = a[t2][t1] = 1;
	}
	cin >> cnt;
	while (cnt--) {
		cin >> k;
		vector<int> v(k);
		set<int> s;
		int flag1 = 1, flag2 = 1;
		for (int i = 0; i < k; i++) {
			scanf("%d", &v[i]);
			s.insert(v[i]);
		}
		//1，该圈的顶点总数不等于图的顶点数(经过筛选，保证该图的每个顶点唯一)
		//2，该圈的顶点数不等于图的顶点数
		//3，起点不等于终点
		if (s.size() != n || k - 1 != n || v[0] != v[k - 1])
			flag1 = 0;
		//判断该图能否形成通路
		//疑问：不一定相邻点要形成通路吧？
		//这是必然， 但是v数组是根据点推入的顺序决定的，所以相邻点必须连通
		for (int i = 0; i < k - 1; i++) {
			if (a[v[i]][v[i + 1]] == 0)
				flag2 = 0;
		}
		printf("%s", flag1&&flag2 ? "YES\n" : "NO\n");
	}
	return 0;
}
```







