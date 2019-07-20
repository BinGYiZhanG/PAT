
一个供应链是一个零售商（retailers），经销商（distributors），和供应商（suppliers）的网络。每个人涉及从供应商到消费者移动产品。<br>
开始于某个根供应商，在链上的每个以价格P从它的供应商那里买产品，并且买或者分发他们以高于价格P r%的价格。只有零售商是面对顾客的。假定在供应链的每个成员有一个确切的供应商除了根供应商之外，没有供应环。<br>
现在给出一个供应链，你应该给出从所有零售商那里的总销售

输入：
N，供应链的成员个数；P，价格；r，利率。

输出：
从供应商i那里收到产品的零售商，或者是经售商的
0--零售商，

保留一位小数，

### BFS
```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

const int maxn=1e5+10;
struct node{
    double p,product;
    vector<int> child;
}Node[maxn];

int n;
double p,r;
double ans=0;
void BFS(int root){
    queue<int> q;
    q.push(root);
    while(!q.empty()){
        int top=q.front();
        q.pop();
        if(Node[top].child.size()){
            for(int i=0;i<(int)Node[top].child.size();i++){
                int child=Node[top].child[i];
                Node[child].p=Node[top].p*(1+r);
                q.push(child);
            }
        }
        else{
            ans+=Node[top].p*Node[top].product;
        }
    }
}

int main(){
    scanf("%d%lf%lf",&n,&p,&r);
    r/=100;
    for(int i=0;i<n;i++){
        int k;
        scanf("%d",&k);
        if(k){
            int x;
            while(k--){
               // for(int i=0;i<k;i++){
                scanf("%d",&x);
                Node[i].child.push_back(x);
               // }
            }
        }
        else{
            scanf("%lf",&Node[i].product);
        }
    }
    Node[0].p=p;
    BFS(0);
    printf("%.1f\n",ans);
    return 0;
}


```

### DFS

```cpp
#include<iostream>
#include<queue>
#include<vector>
using namespace std;
const int maxn = 1e5 + 10;
struct node {
	double p, product;
	vector<int>child;
}Node[maxn];
int n; 
double p, r;
double ans = 0;
void DFS(int index)
{
	if (Node[index].child.size() == 0)
	{
		ans += Node[index].p*Node[index].product;
		return;
	}
	for (int i = 0; i < Node[index].child.size(); i++)
	{
		int child = Node[index].child[i];
		Node[child].p = Node[index].p*(1 + r);
		DFS(child);
	}
}
int main()
{
	scanf("%d%lf%lf", &n, &p, &r);
	r /= 100;
	for (int i = 0; i < n; i++)
	{
		int k;
		scanf("%d", &k);
		if (k)
		{
			while (k--)
			{
				int x;
				scanf("%d", &x);
				Node[i].child.push_back(x);
			}
		}
		else
		{
			scanf("%lf", &Node[i].product);
		}
	}
	Node[0].p = p;
	DFS(0);
	printf("%.1f", ans);
	return 0;
}
```
