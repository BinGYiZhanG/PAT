
### Dijkstra

### 输出：最少花费的路径条数，最少花费，最大快乐值，最大平均快乐值（取整数）

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <map>
#include <algorithm>
#include <string>
using namespace std;

const int MAXV = 210;
const int INF = 1000000000;
int n, m, st, G[MAXV][MAXV], weight[MAXV];
int d[MAXV], w[MAXV], num[MAXV], pt[MAXV], pre[MAXV];
bool vis[MAXV] = { false };
map<string, int> cityToIndex;///城市名 -> 城市编号(0~n-1)
map<int, string> indexToCity;///城市编号(0~n-1) -> 城市名

void Dijkstra(int s) {
	fill(d, d + MAXV, INF);///到起点(编号为0)的最短距离
	fill(w, w + MAXV, 0);///到起点(编号为0)的最短权重
	fill(num, num + MAXV, 0);///到起点(编号为0)的最短路径条数
	fill(pt, pt + MAXV, 0);///记录经过城市（顶点）数
	for (int i = 0; i < n; i++)
		pre[i] = i;
	d[s] = 0;
	w[s] = weight[st];
	num[s] = 1;
	for (int i = 0; i < n; i++) {
		int u = -1, MIN = INF;
		for (int j = 0; j < n; j++) {
			if (vis[j] == false && d[j] < MIN) {
				u = j;
				MIN = d[j];
			}
		}
		if (u == -1)
			return;
		vis[u] = true;
		for (int v = 0; v < n; v++) {
			if (vis[v] == false && G[u][v] != INF) {
				if (d[u] + G[u][v] < d[v]) {///更新最短距离
					d[v] = d[u] + G[u][v];
					w[v] = w[u] + weight[v];
					num[v] = num[u];
					pt[v] = pt[u] + 1;
					pre[v] = u;
				}
				else if (d[u] + G[u][v] == d[v]) {
					num[v] += num[u];///记录最短路径条数
					if (w[u] + weight[v] > w[v]) {///更新最大幸福值
						w[v] = w[u] + weight[v];
						pt[v] = pt[u] + 1;
						pre[v] = u;
					}
					else if (w[u] + weight[v] == w[v]) {
						double uAvg = 1.0*(w[u] + weight[v]) / (pt[u] + 1);
						double vAvg = 1.0*w[v] / pt[v];
						if (uAvg > vAvg) {///更新最大平均幸福值
							pt[v] = pt[u] + 1;
							pre[v] = u;
						}
					}
				}
			}
		}
	}
}

void printPath(int v) {
	if (v == 0) {
		cout << indexToCity[v];
		return;
	}
	printPath(pre[v]);
	cout << "->" << indexToCity[v];
}
int main() {
	string start, city1, city2;
	cin >> n >> m >> start;///城市个数: n, 道路条数：m, 起始城市姓名: 
	cityToIndex[start] = 0;
	indexToCity[0] = start;
	for (int i = 1; i <= n - 1; i++) {
		cin >> city1 >> weight[i];
		cityToIndex[city1] = i;     ///城市名 ->  城市编号
		indexToCity[i] = city1;     ///城市编号 -> 城市名
	}
	fill(G[0], G[0] + MAXV * MAXV, INF);///每条道路权值置为无穷大
	for (int i = 0; i < m; i++) {///输入每条道路权值
		cin >> city1 >> city2;
		int c1 = cityToIndex[city1], c2 = cityToIndex[city2];
		cin >> G[c1][c2];
		G[c2][c1] = G[c1][c2];
	}
	Dijkstra(0);
	int rom = cityToIndex["ROM"];
	printf("%d %d %d %d\n", num[rom], d[rom], w[rom], w[rom] / pt[rom]);
	///输出：最少花费的路径条数，最少花费，最大快乐值，最大平均快乐值（取整数）
	printPath(rom);
	return 0;
}

```
