* A proper vertex coloring is a labeling of the graph's vertices with colors such that no two vertices sharing the same edge have the same color. A coloring using at most k colors is called a (proper) k-coloring.
* Now you are supposed to tell if a given coloring is a proper k-coloring.

### 输入：
* 第一行，N and M (both no more than 10^{4}), being the total numbers of vertices and edges, 
* 接下来M行，ach describes an edge by giving the indices (from 0 to N−1) of the two ends of the edge.
* K,which is the number of colorings you are supposed to check
* Then K lines follow, each contains N colors which are represented by non-negative integers in the range of int. The i-th color is the color of the i-th vertex.

### 输出：
* For each coloring, print in a line k-coloring if it is a proper k-coloring for some positive k, or No if not.

### 思路：
* 存边，构造图


