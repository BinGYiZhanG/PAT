微博被称为中国版的Twitter。一个用户在微博上可能有很多粉丝，也可能关注很多其他用户。因此，一个社交网络是由追随者关系形成的。当用户在微博上发帖时，他/她的所有追随者都可以查看和转发他/她的帖子，然后他/她的追随者可以再次转发他/她的帖子。现在给定一个社交网络，假设只计算L个级别的间接追随者，您应该计算任何特定用户的最大转发潜在数量。<br>

输入：
N，用户数量；L，被计算的间接追随者级别的数量。

K，K个查询，
输出：
对于每个用户id，您应该在一行中打印该用户能够触发的转发的最大潜在数量，假设每个能够查看初始帖子的人都会转发一次，并且只计算L个级别的间接关注者。

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <vector>
#include <queue>
using namespace std;

const int MAXV = 1010;
struct Node {
	int id;
	int layer;
};
vector<Node> Adj[MAXV];
bool inq[MAXV] = { false };

int BFS(int s, int L) {
	int numForward = 0;
	queue<Node> q;
	Node start;
	start.id = s;
	start.layer = 0;
	q.push(start);
	inq[start.id] = true;
	while (!q.empty()) {
		Node topNode = q.front();
		q.pop();
		int u = topNode.id;
		for (int i = 0; i < Adj[u].size(); i++) {
			Node next = Adj[u][i];
			next.layer = topNode.layer + 1;
			if (inq[next.id] == false && next.layer <= L) {
				q.push(next);
				inq[next.id] = true;
				numForward++;
			}
		}
	}
	return numForward;
}



int main() {
	Node user;
	int n, L, numFollow, idFollow;
	scanf("%d%d", &n, &L);
	for (int i = 1; i <= n; i++) {
		user.id = i;
		scanf("%d", &numFollow);
		for (int j = 0; j < numFollow; j++) {
			scanf("%d", &idFollow);
			Adj[idFollow].push_back(user);
		}
	}
	int numQuery, s;
	scanf("%d", &numQuery);
	for (int i = 0; i < numQuery; i++) {
		fill(inq, inq + MAXV, false);
		scanf("%d", &s);
		int numForward = BFS(s, L);
		printf("%d\n", numForward);
	}
	return 0;
}

```
