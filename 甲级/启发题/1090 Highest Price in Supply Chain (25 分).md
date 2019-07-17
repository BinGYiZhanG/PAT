
一个供应链是一个零售商，经销商，和供应商的网络，每个人涉及从供应商到顾客的移动产品流程。<br>
开始于一个根供应商(root supplier),在链上的每一个人从各自的供应商那里以价格P买入产品，并且售卖或者分发他们以高于价格P r%的价格，假定在供应链上的每个成员都有一个确切的供应商除了根供应商，并且没有供应环。<br>
现在给出一个供应链，你应该得到最高价格从一些零售商那里<br>

### 输入:
N,供应链上的成员个数，P，给出的根供应商的价格，r，利率，

### 输出
输出我们期望的最高价格，保留两位小数，零售商的数目。

```cpp
#include <cstdio>
#include <cmath>
#include <vector>

using namespace std;
const int maxn = 100010;
vector<int> child[maxn];
double p, r;

int num = 0, maxDepth = 0, n;
void DFS(int index, int depth) {
	if (child[index].size() == 0) {
		if (depth > maxDepth) {
			maxDepth = depth;
			num = 1;
		}
		else if (depth == maxDepth) {
			num++;
		}
		return;
	}
	for (int i = 0; i < child[index].size(); i++) {
		DFS(child[index][i], depth + 1);
	}
	
}

int main() {
	int father, root;
	scanf("%d%lf%lf", &n, &p, &r);
	r /= 100;
	for (int i = 0; i < n; i++) {
		scanf("%d", &father);
		if (father != -1) {
			child[father].push_back(i);
		}
		else {
			root = i;
		}
	}
	DFS(root, 0);
	printf("%.2f %d\n", p*pow(1 + r, maxDepth), num);
	return 0;
}
```



