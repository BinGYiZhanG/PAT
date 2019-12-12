不像今天，在早些年，男孩儿女孩儿们表达爱意是非常微妙的，当一个男孩A暗恋一个女孩B，他通常不会直接去联系她。<br>
相反，他或许回去询问另一个男孩C，一个她最亲近的朋友,来询问另一个女孩D，同时是B和C的朋友，相当长一番行动吧，不是吗？<br>
女孩也会做类似的事。<br>

现在给出一个朋友网，你应该帮助一个男孩或者女孩列出能够帮助他们做出第一个联系的全部朋友。<br>

### 输出：
* 第一行，N，总人数，M，朋友关系数。
* 接下来M行，每行给出一对朋友，

负数表示女孩，ID是4位整数<br>
* K，查询个数，
* 接下来K行，每行给出一对爱人，假定是第一个暗恋第二个。

### 输出：
对于每对查询，首先打印对数，<br>
接下来打印其ID<br>
如果爱人A，B是相反性别，你应该首先打印与A性别相同的朋友，然后打印与B性别相同的朋友<br>
如果恋人A,B是相同性别，你应该打印所有他们相同性别的朋友，保证每个人只有一种性别<br>

按递增序打印，一对的两个的ID，按照递增打印<br>


```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
#include <unordered_map>
using namespace std;

unordered_map<int, bool> arr;

struct node {
	int a, b;
};
bool cmp(node x, node y) {
	if (x.a != y.a)
		return x.a < y.a;
	else
		return x.b < y.b;
}
int main() {
	int n, m, k;
	scanf("%d%d", &n, &m);
	vector<int> v[10000];
	for (int i = 0; i < m; i++) {
		//如果用int接收一对朋友，-0000和0000对于int来说都是0，
		//将无法得知这个人的性别，也就会影响他找他的同性朋友的那个步骤，
		//所以考虑用字符串接收，
		string a, b;
		cin >> a >> b;
		if (a.length() == b.length()) {
			v[abs(stoi(a))].push_back(abs(stoi(b)));
			v[abs(stoi(b))].push_back(abs(stoi(a)));
		}
		//疑问1:如果对女生id取绝对值，会不会与男生的id重复?每个人都有独一无二的ID
		arr[abs(stoi(a)) * 10000 + abs(stoi(b))] = arr[abs(stoi(b)) * 10000 + abs(stoi(a))] = true;
		//用数组arr标记两个人是否是朋友（邻接矩阵表示）
	}
	scanf("%d", &k);
	for (int i = 0; i < k; i++) {
		int c, d;
		cin >> c >> d;
		vector<node> ans;
		for (int j = 0; j < v[abs(c)].size(); j++) {
			for (int k = 0; k < v[abs(d)].size(); k++) {
				if (v[abs(c)][j] == abs(d) || abs(c) == v[abs(d)][k])continue;
				//A在寻找同性朋友时，需要避免找到他想要的伴侣B，
				//所以当当前朋友就是B或者B的同性朋友就是A时舍弃该结果
				if (arr[v[abs(c)][j] * 10000 + v[abs(d)][k]] == true)
				//对于一对想要在一起的A和B，他们需要先找A的所有同性朋友C，
				//再找B的所有同性朋友D，当C和D两人是朋友的时候则可以输出C和D
					ans.push_back(node{ v[abs(c)][j],v[abs(d)][k] });
			}
		}
		sort(ans.begin(), ans.end(), cmp);
		printf("%d\n", int(ans.size()));
		for (int j = 0; j < ans.size(); j++)
			printf("%04d %04d\n", ans[j].a, ans[j].b);
	}
	return 0;
}
```
