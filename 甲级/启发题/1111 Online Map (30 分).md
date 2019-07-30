输出我们目前的位置和一个目的地，一个在线地图会推荐几条道路。现在你的工作是向你的用户推荐两条路：一条是最短的，另一条是最快的。保证对于任何需求的道路是存在的。

### 输入：

每一个输入文件包含一个测试用例。对于每一个例子，<br>
第一行，N，在一张地图上的街道十字的总数；M，街道数量。<br>
接下来M行，每行描述一条街的格式是：<br>
```
V1 V2 one-way length time
```
```V1```和```V2```是一条街的两个端点；<br>
```one-way```如果是1，则代表从```V1```到```V2```有街道，如果是0，则代表没街道;<br>
```length```是街道的长度；<br>
```time```通过街道的时间<br>
最后给出一对源点和目的地

### 输出：

对于每一个示例，首先打印从源点到目的地的最短路径和最短距离```D```以下面格式:
```
Distance = D: source -> v1 -> ... -> destination
```
然后下一行给出最快路径和最短时间```T```:
```
Time = T: source -> w1 -> ... -> destination
```
在示例中，如果最短路径不是唯一的，输出最快到达的那条，这保证是唯一的。如果最快路径不是唯一的，输出经过最少的交叉点的那条，这保证是唯一的。
```
Distance = D; Time = T: source -> u1 -> ... -> destination
```
```cpp
#include <iostream>
#include <algorithm>
#include <vector>
//#pragma warning (disable:4996)
using namespace std;
const int inf = 999999999;//9个9
int dis[510], Time[510], e[510][510], w[510][510], dispre[510], Timepre[510]
,weight[510],NodeNum[510];
bool vis[510];

vector<int> dispath, Timepath, tempath;
int st, fin, minnode = inf;
void dfsdiapath(int v) {
	dispath.push_back(v);
	if (v == st)	return;
	dfsdiapath(dispre[v]);
}

void dfsTimepath(int v) {
	Timepath.push_back(v);
	if (v == st)	return;
	dfsTimepath(Timepre[v]);
}

int main() {
	fill(dis, dis + 510, inf);
	fill(Time, Time + 510, inf);
	fill(weight, weight + 510, inf);
	fill(e[0], e[0] + 510 * 510, inf);
	fill(w[0], w[0] + 510 * 510, inf);
	int n, m;
	scanf("%d%d", &n, &m);
	int a, b, flag, len, t;
	for (int i = 0; i < m; i++) {
		scanf("%d %d %d %d %d", &a, &b, &flag, &len, &t);
		e[a][b] = len;
		w[a][b] = t;
		if (flag != 1) {
			e[b][a] = len;
			w[b][a] = t;
		}
	}

	scanf("%d %d", &st, &fin);
	dis[st] = 0;
	for (int i = 0; i < n; i++)
		dispre[i] = i;
	for (int i = 0; i < n; i++) {
		int u = -1, minn = inf;
		for (int j = 0; j < n; j++) {
			if (vis[j] == false && dis[j] < minn) {
				u = j;
				minn = dis[j];
			}
		}
		if (u == -1)	break;
		vis[u] = true;

		for (int v = 0; v < n; v++) {
			if (vis[v] == false && e[u][v] != inf) {
				if (e[u][v] + dis[u] < dis[v]) {
					dis[v] = dis[u] + e[u][v];
					dispre[v] = u;
					weight[v] = weight[u] + w[u][v];
				}
				else if (e[u][v] + dis[u] == dis[v] && weight[v] > weight[u] + w[u][v]) {
					weight[v] = weight[u] + w[u][v];
					dispre[v] = u;
				}
			}
		}
	}


	dfsdiapath(fin);

	Time[st] = 0;
	fill(vis, vis + 510, false);
	for (int i = 0; i < n; i++) {
		int u = -1, minn = inf;
		for (int j = 0; j < n; j++) {
			if (vis[j] == false && minn > Time[j]) {
				u = j;
				minn = Time[j];
			}
		}
		if (u == -1)	break;
		vis[u] = true;
		for (int v = 0; v < n; v++) {
			if (vis[v] == false && w[u][v] != inf) {
				if (w[u][v] + Time[u] < Time[v]) {
					Time[v] = w[u][v] + Time[u];
					Timepre[v] = u;
					NodeNum[v] = NodeNum[u] + 1;
				}
				else if (w[u][v] + Time[u] == Time[v] && NodeNum[u] + 1 < NodeNum[v]) {
					Timepre[v] = u;
					NodeNum[v] = NodeNum[u] + 1;
				}
			}
		}
	}

	dfsTimepath(fin);

	printf("Distance = %d", dis[fin]);
	if (dispath == Timepath) {
		printf("; Time = %d: ", Time[fin]);
	}
	else {
		printf(": ");
		for (int i = dispath.size() - 1; i >= 0; i--) {
			printf("%d", dispath[i]);
			if (i != 0)	printf(" -> ");
		}
		printf("\nTime = %d: ", Time[fin]);
	}
	for (int i = Timepath.size() - 1; i >= 0; i--) {
		printf("%d", Timepath[i]);
		if (i != 0)printf(" -> ");
	}
	return 0;
}
```
