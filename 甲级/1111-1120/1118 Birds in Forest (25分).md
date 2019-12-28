
* 注意：
  * 所有的数组必须得先初始化，```memset```
  

```
#include <bits/stdc++.h>

using namespace std;

int father[10010],cnt[10010];
bool exists[10010];
int findFather(int x){
    int a=x;
    while(x!=father[x])
        x=father[x];

    while(a!=father[a]){
        int z=a;
        a=father[a];
        father[z]=x;
    }
    return x;
}


void Union(int a, int b) {
	int faA = findFather(a);
	int faB = findFather(b);
	if (faA != faB)
		father[faA] = faB;
}

int N,K,Q;
///让最小的当根也不是一个好的方法，
int main(){
    scanf("%d",&N);
    int maxn=0;
    memset(exists,false,sizeof(exists));
    memset(cnt,0,sizeof(cnt));
    for(int i=1;i<=10010;i++)
        father[i]=i;
    for(int i=0;i<N;i++){
        scanf("%d",&K);
        int root;
        if(K>0)
            scanf("%d",&root),exists[root]=true,maxn=max(maxn,root);
        for(int j=0;j<K-1;j++){
            int tmpc;
            scanf("%d",&tmpc);
            Union(root,tmpc);
            exists[tmpc]=true;
            maxn=max(maxn,tmpc);
        }
    }

    for(int i=1;i<=maxn;i++){
        if(exists[i]==true){
            int Root=findFather(i);
            cnt[Root]++;///记录该棵树的鸟数
           // printf("%d\n",Root);
        }
    }

    int maxntree=0,maxbirds=0;
    for(int i=1;i<=maxn;i++){
        if(exists[i]==true&&cnt[i]!=0){
            maxntree++;
            maxbirds+=cnt[i];
        }
    }

    scanf("%d",&Q);
    printf("%d %d\n",maxntree,maxbirds);
    for(int i=0;i<Q;i++){
        int a,b;
        scanf("%d%d",&a,&b);
        if(findFather(a)!=findFather(b))
            printf("No\n");
        else
            printf("Yes\n");
    }

}


```

