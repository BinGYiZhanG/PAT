#### 贴一个19分代码，用SPFA写的
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>
#include <queue>
using namespace std;

const int MAXV = 510;
const int INF = 1000000000;
struct Node {
	int v, dis;
	Node(int _v,int _dis):v(_v),dis(_dis){}
};

vector<Node> Adj[MAXV];
int n, m, st, ed, G[MAXV][MAXV], weight[MAXV];
int d[MAXV], w[MAXV], num[MAXV];
bool vis[MAXV] = { false };
bool inq[MAXV] = { false };
void Dijkstra(int s) {
	fill(d, d + MAXV, INF);
	fill(num, num + MAXV, 0);
	fill(w, w + MAXV, 0);
	d[s] = 0;
	w[s] = weight[s];
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
				if (d[u] + G[u][v] < d[v]) {
					d[v] = d[u] + G[u][v];
					w[v] = w[u] + weight[v];
					num[v] = num[u];
				}
				else if (d[u] + G[u][v] == d[v]) {
					if (w[u] + weight[v] > w[v]) {
						w[v] = w[u] + weight[v];
					}
					num[v] += num[u];
				}
			}
		}
	}
}


bool SPFA_primitive(int s) {
	fill(inq, inq + MAXV, false);
	fill(num, num + MAXV, 0);
	fill(d, d + MAXV, INF);
	queue<int> Q;
	Q.push(s);
	inq[s] = true;
	num[s]++;
	d[s] = 0;
	while (!Q.empty()) {
		int u = Q.front();
		Q.pop();
		inq[u] = false;
		for (int j = 0; j < Adj[u].size(); j++) {
			int v = Adj[u][j].v;
			int dis = Adj[u][j].dis;
			if (d[u] + dis < d[v]) {
				d[v] = d[u] + dis;
				if (!inq[v]) {
					Q.push(v);
					inq[v] = true;
					num[v]++;
					if (num[v] >= n)
						return false;
				}
			}
		}
	}
	return true;
}

void SPFA(int s) {
	fill(inq, inq + MAXV, false);
	fill(num, num + MAXV, 0);
	fill(d, d + MAXV, INF);
	queue<int> Q;
	Q.push(s);
	inq[s] = true;
	num[s]=1;
	d[s] = 0;
	w[s] = weight[s];
	while (!Q.empty()) {
		int u = Q.front();
		Q.pop();
		inq[u] = false;
		for (int j = 0; j < Adj[u].size(); j++) {
			int v = Adj[u][j].v;
			int dis = Adj[u][j].dis;
			if (d[u] + dis < d[v]) {
				d[v] = d[u] + dis;
				w[v] = w[u] + weight[v];
;				if (!inq[v]) {
					Q.push(v);
					inq[v] = true;
				}
				num[v] = num[u];
			}
			else if (d[u] + dis == d[v]) {
				if (w[u] + weight[v] > w[v]) {
					w[v] = w[u] + weight[v];
				}
				if (!inq[v]) {
					Q.push(v);
					inq[v] = true;
				}
				num[v] += num[u];
			}
		}
	}
	
}

//19分代码          1003	Emergency
int main() {
	scanf_s("%d%d%d%d", &n, &m, &st, &ed);
	for (int i = 0; i < n; i++) {
		scanf_s("%d", &weight[i]);
	}
	int u, v,dis;
	fill(G[0], G[0] + MAXV * MAXV, INF);
	for (int i = 0; i < m; i++) {
		scanf_s("%d%d%d", &u, &v, &dis);
		Adj[u].push_back(Node(v, dis));
		Adj[v].push_back(Node(u, dis));
	}
	//for (int i = 0; i < m; i++) {
	//	scanf_s("%d%d", &u, &v);
	//	scanf_s("%d", &G[u][v]);
	//	G[v][u] = G[u][v];
	//}
	SPFA(st);
//	Dijkstra(st);
	printf("%d %d\n", num[ed], w[ed]);
	return 0;
}
```

