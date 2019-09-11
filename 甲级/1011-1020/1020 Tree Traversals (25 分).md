### 模板题

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <queue>
#include <algorithm>
using namespace std;
struct node {
	int data;
	node* lchild;
	node* rchild;
};
const int maxn = 50;
int post[maxn], in[maxn], pre[maxn];
int n;

node* create(int postL, int postR, int inL, int inR) {
	if (postL > postR)
		return NULL;
	node* root = new node;
	root->data = post[postR];
	int k;
	for (k = inL; k < inR; k++) {
		if (in[k] == root->data)
			break;
	}
	int numLeft = k - inL;
	root->lchild = create(postL, postL + numLeft - 1, inL, k - 1);
	root->rchild = create(postL + numLeft, postR - 1, k + 1, inR);
	return root;
}

int num = 0;
void BFS(node* root) {
	queue<node*> q;
	q.push(root);
	while (!q.empty()) {
		node* now = q.front();
		q.pop();
		printf("%d", now->data);
		num++;
		if (num < n)
			printf(" ");
		if (now->lchild)
			q.push(now->lchild);
		if (now->rchild)
			q.push(now->rchild);
	}
}
int main() {
	cin >> n;
	for (int i = 0; i < n; i++)
		cin >> post[i];
	for (int i = 0; i < n; i++)
		cin >> in[i];
	node* root = create(0, n - 1, 0, n - 1);
	BFS(root);
	return 0;
}
```
