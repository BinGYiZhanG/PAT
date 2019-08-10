一种平衡二叉树叫做红黑树，它有下列5中性质：
* 1，所有结点非红即黑
* 2，根为黑
* 3，每个叶子为黑（不对）
* 4，如果一个结点为红，它的所有孩子为黑
* 5，从任意结点到叶⼦子结点的路路径中，⿊黑⾊色结点的个数是否相同

现在给出一棵二叉树，你应该判断它是否是一棵合法的红黑树。
### 输入
* 第一行，K，测试用例数目
* 对于每个测试用例，
  * 第一行，N，二叉树的结点数目，
  * 第二行，树的前序遍历
正数---黑结点；负数---红结点


### 输出：
是，输出“Yes”；否，输出“No”

```cpp
#include <iostream>
#include <cstdio>
#include <cmath>
#include <vector>
#include <algorithm>
using namespace std;

//1，所有结点非红即黑
//2，根为黑
//3，每个叶子为黑
//4，如果一个结点为红，它的所有孩子为黑
//5，对于每个结点，包含相同数目的黑结点
vector<int> arr;
struct node {
	int val;
	struct node *left, *right;
};

node* build(node *root, int v) {
	if (root == NULL) {
		root = new node();
		root->val = v;
		root->left = root->right = NULL;
	}
	else if (abs(v) <= abs(root->val))
		root->left = build(root->left, v);
	else
		root->right = build(root->right, v);
	return root;
}

//2. 根据建立的树，从根结点开始遍历，
//如果当前结点是红色，判断它的孩子节点是否为黑色，递归返回结果【judge1函数】
//疑问1:如果当前结点为黑色，他的孩子必须是红色吗?不是必须的，孩子结点可以全黑,测试一下即可
bool judge1(node *root) {
	if (root == NULL)
		return true;
	if (root->val < 0) {
		if (root->left != NULL && root->left->val < 0)
			return false;
		if (root->right != NULL && root->right->val < 0)
			return false;
	}
	return judge1(root->left) && judge1(root->right);
}

//求出黑色结点的个数
int getNum(node *root) {
	if (root == NULL)
		return 0;
	int l = getNum(root->left);
	int r = getNum(root->right);
	return root->val > 0 ? max(l, r) + 1 : max(l, r);
	//记录黑结点
}

//从根节点开始，递归遍历，
//检查每个结点的左子树的高度和右子树的高度（这里的高度指黑色结点的个数），
//比较左右孩子高度是否相等（即，判断条件5），递归返回结果
bool judge2(node *root) {
	if (root == NULL)
		return true;
	int l = getNum(root->left);
	int r = getNum(root->right);
	if (l != r)
		return false;
	return judge2(root->left) && judge2(root->right);
}

int main() {
	int k, n;
	scanf("%d", &k);
	for (int i = 0; i < k; i++) {
		scanf("%d", &n);
		arr.resize(n);
		node *root = NULL;
		for (int j = 0; j < n; j++) {
			scanf("%d", &arr[j]);
			root = build(root, arr[j]);
		}
		if (arr[0] < 0 || judge1(root) == false || judge2(root) == false)
			printf("No\n");
		else
			printf("Yes\n");
	}
	return 0;
}
```
