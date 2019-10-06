* Your job is to check every path in a given complete binary tree, in order to tell if it is a heap or not.

### 输入：
* 第一行，N，the number of keys in the tree.
* 下一行，N distinct integer keys (all in the range of int), which gives the level order traversal sequence of a complete binary tree.

### 输出：
* for each node in the tree, all the paths in its right subtree must be printed before those in its left subtree.
* Finally print in a line Max Heap if it is a max heap, or Min Heap for a min heap, or Not Heap if it is not a heap at all.

### 思路：
* 先序遍历的镜像
* 大/小顶堆的判断


