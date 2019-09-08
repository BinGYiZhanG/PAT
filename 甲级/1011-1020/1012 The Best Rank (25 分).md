### 题目大意：
* 现已知n个考生的3门分数，平均分可以按照这三门算出来。然后分别对这四个分数从高到低排序，这样对每个考⽣生来说有4个排名。
* k个查询，对于每一个学生id，输出当前id学生的最好的排名和它对应的分数，
* 如果名次相同，按照A>C>M>E的顺序输出～如果当前id不存在，输出N/A～

#### 本题难点:对于每个同学的成绩排序

#### 思路：
* ```vector<pair<string, double> > vec; ```记录 学号 & 成绩
* ```vec.push_back(make_pair(stu[i].num, stu[i].a));``` 推入 学号 & 成绩
* ```bool cmp1(const pair<string, double>&p1, const pair<string, double>&p2)``` 排序 学号 & 成绩


```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <string>
#include <algorithm>
#include <map>
#include <set>
using namespace std;

//本题难点:对于每个同学的成绩排序
const int maxn = 2010;
struct stu {
	string num;
	int c;
	int m;
	int e;
	int a;
}stu[maxn];


bool cmp(const pair<string, int>&p1, const pair<string, int>&p2) {
	return p1.second > p2.second;
}
bool cmp1(const pair<string, double>&p1, const pair<string, double>&p2) {
	return p1.second > p2.second;
}

int main(){
	int n, m;
	cin >> n >> m;
	set<string> stu_num;//存储学生的姓名，判断输入姓名是否合法
	vector<pair<string, int> > vec1,vec2,vec3;
	vector<pair<string, double> > vec;
	for (int i = 0; i < n; i++) {
		cin >> stu[i].num >> stu[i].c >> stu[i].m >> stu[i].e;
		stu[i].a = (stu[i].c + stu[i].m + stu[i].e) / 3.0 + 0.5;
		vec1.push_back(make_pair(stu[i].num, stu[i].c));
		vec2.push_back(make_pair(stu[i].num, stu[i].m));
		vec3.push_back(make_pair(stu[i].num, stu[i].e));
		vec.push_back(make_pair(stu[i].num, stu[i].a));
		stu_num.insert(stu[i].num);
	}
	sort(vec1.begin(), vec1.end(), cmp);
	//存储学生在c的排名

	map<string, int> rank1;
	rank1[vec1[0].first] = 1;
	for (int i = 1; i < vec1.size(); i++) {
		if (vec1[i].second != vec1[i - 1].second)
			rank1[vec1[i].first] = i + 1;
		else
			rank1[vec1[i].first] = rank1[vec1[i-1].first];
	}
	
	sort(vec2.begin(), vec2.end(), cmp);
	//存储学生在m的排名
	map<string, int> rank2;
	rank2[vec2[0].first] = 1;
	for (int i = 1; i < vec2.size(); i++) {
		if (vec2[i].second != vec2[i - 1].second)
			rank2[vec2[i].first] = i + 1;
		else
			rank2[vec2[i].first] = rank2[vec2[i - 1].first];
	}


	sort(vec3.begin(), vec3.end(), cmp);
	//存储学生在e的排名

	map<string, int> rank3;
	rank3[vec3[0].first] = 1;
	for (int i = 1; i < vec3.size(); i++) {
		if (vec3[i].second != vec3[i - 1].second)
			rank3[vec3[i].first] = i + 1;
		else
			rank3[vec3[i].first] = rank3[vec3[i - 1].first];
	}


	sort(vec.begin(), vec.end(), cmp1);
	//存储学生在a的排名

	map<string, int> rank;
	rank[vec[0].first] = 1;
	for (int i = 1; i < vec.size(); i++) {
		if (vec[i].second != vec[i - 1].second)
			rank[vec[i].first] = i + 1;
		else
			rank[vec[i].first] = rank[vec[i - 1].first];
	}


	for (int i = 0; i < m; i++) {
		string str;
		cin >> str;
		if (stu_num.find(str) == stu_num.end()) {
			printf("N/A\n");
			continue;
		}
		int a = rank1[str], b = rank2[str], c = rank3[str],A=rank[str];
		int max_ = min(A,min(a, min(b, c)));
		if (max_ == A) {
			printf("%d A\n",max_);
		}
		else if (max_ == a) {
			printf("%d C\n", max_);
		}
		else if (max_ == b) {
			printf("%d M\n", max_);
		}
		else if (max_ == c) {
			printf("%d E\n", max_);
		}
	}

}
```
