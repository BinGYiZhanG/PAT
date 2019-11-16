
### 推入时，前序遍历
### 推出时，中序遍历

![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/A1086.jpg)
```
前序 DLR 
推入： 1 2 3 4 5 6
中序 LDR
推出： 3 2 4 1 6 5

```

```cpp
#include <iostream>
#include <stack>
#include <cstdio>
#include <string>
using namespace std;

const int maxn = 35;
int n;
int post[maxn], in[maxn], pre[maxn];
struct node {
	int data;
	node* lchild;
	node* rchild;
};

//先序和中序，那叫构建树,而非求出后序
node* create(int preL, int preR, int inL, int inR) {
	if (preL > preR)
		return NULL;
	node* root = new node;
	root->data = pre[preL];
	int k;
	for (k = inL; k < inR; k++) {
		if (in[k] == root->data)
			break;
	}
	int numLeft = k - inL;
	root->lchild = create(preL + 1, preL + numLeft, inL, k - 1);
	root->rchild = create(preL + numLeft + 1, preR, k + 1, inR);
	return root;
}

int num = 0;
void postorder(node* root) {///后序输出
	if (root == NULL)
		return;
	postorder(root->lchild);
	postorder(root->rchild);
	printf("%d", root->data);
	num++;
	if (num < n)
		printf(" ");
}

int main() {
	stack<int> st;
	string str;
	cin >> n;
	int prenum = 0, innum = 0;
	getchar();
	while (getline(cin, str)) {
		if (str[1] == 'u') {//Push
			string nums = str.substr(4);
			int num = atoi(nums.c_str());
			st.push(num);
			pre[prenum++] = num;
		}
		else {//Pop
			int num = st.top();
			st.pop();
			in[innum++] = num;
		}
		if (innum == n)//控制结束循环
			break;
	}
	node* root = create(0, n - 1, 0, n - 1);///起止端点是数组中的元素
	postorder(root);
	
	
	/*for (int i = 0; i < prenum; i++) {
		if (i != 0)
			printf(" ");
		printf("%d", pre[i]);
	}

	cout << endl;
	for (int i = 0; i < innum; i++) {
		if (i != 0)
			printf(" ");
		printf("%d", in[i]);
	}
	cout << endl;*/
	return 0;
}
```
