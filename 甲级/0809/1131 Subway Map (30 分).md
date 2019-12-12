在大城市里，地铁系统对于旅客来说看起来很复杂。给你一些感觉，接下来这张图展示了北京地铁地图。现在你应该帮助人们利用你的计算能力！<br>
给出你的用户的起点，你的任务是发现到达目的地的最快方式。<br>

### 输入：
第一行，N，地铁线数，
接下来N行，第i行表述了第i个地铁以如下格式：
```
M S[1] S[2]...S[M]
```
M,是站点数目，S[i]是站的标号（从0000到9999）。保证车站被给的顺序正确---也就是说，在S[i]~S[i+1]没有任何的停站。<br>
#### 注意：
* 可能存在循环，但不是自循环（没有地铁从S到S中间不经过其他站）。
* 每个车站间隔属于一个唯一的地铁站线。
* 尽管这些地铁线或许会经过彼此在一些车站（所谓的“中转站”），没有车站连接超过5条线。

在描述完地铁之后，K，<br>
接下来的K行，代表你的用户给出的查询：给出两个下标，起点站和终点站。<br>
保证所有可达，所有查询包含合法车站号。<br>

### 输出：
```
Take Line#X1 from S1 to S2.
Take Line#X2 from S2 to S3.
......
```

### Sample Input:
```
4
7 1001 3212 1003 1204 1005 1306 7797
9 9988 2333 1204 2006 2005 2004 2003 2302 2001
13 3011 3812 3013 3001 1306 3003 2333 3066 3212 3008 2302 3010 3011
4 6666 8432 4011 1306
3
3011 3013
6666 2001
2004 3001
```
### Sample Output:
```
2
Take Line#3 from 3011 to 3013.
10
Take Line#4 from 6666 to 1306.
Take Line#3 from 1306 to 2302.
Take Line#2 from 2302 to 2001.
6
Take Line#2 from 2004 to 1204.
Take Line#1 from 1204 to 1306.
Take Line#3 from 1306 to 3001.

```

```
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;
vector<vector<int>> v(10000);
int visit[10000], minCnt, minTransfer, start, end1;
unordered_map<int, int> line;
vector<int> path, tempPath;

// 计算数组a中的站点所属的站线条数
// 如果该站点的站线值不等于前一个站点的站线值，则cnt加1 
int transferCnt(vector<int> a) {
    int cnt = -1, preLine = 0;
    for (int i = 1; i < a.size(); i++) {
        if (line[a[i-1]*10000+a[i]] != preLine) cnt++;
        preLine = line[a[i-1]*10000+a[i]];
    }
    return cnt;
}
void dfs(int node, int cnt) {
    if (node == end1 && (cnt < minCnt || (cnt == minCnt && transferCnt(tempPath) < minTransfer))) {
    //到达终点，经过站点少，或者经过站点相等但是中转站数小
        minCnt = cnt;
        minTransfer = transferCnt(tempPath);
        path = tempPath;
    }
    if (node == end1) return;
    for (int i = 0; i < v[node].size(); i++) {
        if (visit[v[node][i]] == 0) {
            visit[v[node][i]] = 1;
            tempPath.push_back(v[node][i]);///推入该条站点node所连接的下一个站点
            dfs(v[node][i], cnt + 1);
            visit[v[node][i]] = 0;///置未访问过
            tempPath.pop_back();///弹出，
        }
    }
}
int main() {
    int n, m, k, pre, temp;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d%d", &m, &pre);
        for (int j = 1; j < m; j++) {
            scanf("%d", &temp);
            v[pre].push_back(temp);
            v[temp].push_back(pre);
            line[pre*10000+temp] = line[temp*10000+pre] = i + 1;
            pre = temp;
        }
    }
    scanf("%d", &k);
    for (int i = 0; i < k; i++) {
        scanf("%d%d", &start, &end1);
        minCnt = 99999, minTransfer = 99999;
        tempPath.clear();
        tempPath.push_back(start);
        visit[start] = 1;
        dfs(start, 0);
        visit[start] = 0;
        printf("%d\n", minCnt);
        int preLine = 0, preTransfer = start;
        for (int j = 1; j < path.size(); j++) {
            if (line[path[j-1]*10000+path[j]] != preLine) {
                if (preLine != 0) printf("Take Line#%d from %04d to %04d.\n", preLine, preTransfer, path[j-1]);
                preLine = line[path[j-1]*10000+path[j]];
                preTransfer = path[j-1];
            }
        }
        printf("Take Line#%d from %04d to %04d.\n", preLine, preTransfer, end1);
    }
    return 0;
}
```




