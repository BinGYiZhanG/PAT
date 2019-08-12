一个clique是一个无向图的点的集合在clique中的没两个点是邻接的。一个最大clique是一个通过包含邻接点不能进行扩展的clique。<br>
现在你的工作是判断一个被给的点集合是否是一个最大clique。<br>

### 输入
对于每个样例，<br>
* 第一行，Nv，图中的顶点数目；Ne，图中的无向边数。
* 接下来Ne行，是每条边，边的结点序号是从1~Nv。
在图之后，M，是M个需要判断的clique<br>
接下来M行,第一个数是K，代表每个clique的顶点数，然后是其中的点<br>

### 输出：
对于M个查询，
* 如果是```maximal clique```,输出```Yes```
* 如果不是```maximal clique```，但是一个```clique```,输出```Not Maximal```
* 如果不是```clique```,输出```Not a Clique```

### Sample Input:
```
8 10
5 6
7 8
6 4
3 6
4 5
2 3
8 2
2 7
5 3
3 4
6
4 5 4 3 6
3 2 8 7
2 2 3
1 1
3 4 3 6
3 3 2 1
```
### Sample Output:
```
Yes
Yes
Yes
Yes
Not Maximal
Not a Clique
```





