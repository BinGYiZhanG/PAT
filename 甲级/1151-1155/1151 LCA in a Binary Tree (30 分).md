* The lowest common ancestor (LCA) of two nodes U and V in a tree is the deepest node that has both U and V as descendants.Given any two nodes in a binary tree, you are supposed to find their LCA.



### 输出：

* print in a line ```LCA of U and V is A.``` if the LCA is found and A is the key
* But if ```A``` is one of ```U``` and ```V```, print ```X is an ancestor of Y.``` where ```X``` is ```A``` and ```Y``` is the other node
*  If ```U``` or ```V``` is not found in the binary tree, print in a line ```ERROR: U is not found.``` or ```ERROR: V is not found.``` or ```ERROR: U and V are not found.```


### 思路：

* 建树

* 寻找结点```u```与结点```v```的关系
```cpp
//关键步骤
node* LCA(node* root, int u, int v) {
	if (root == NULL)
		return NULL;
	if (root->data == u || root->data == v)
		return root;
	node* left = LCA(root->lchild, u, v);
	node* right = LCA(root->rchild, u, v);
	if (left != NULL && right != NULL)
		return root;
	return left == NULL ? right : left;
}
```


