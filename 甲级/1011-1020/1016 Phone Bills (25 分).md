### 大模拟

```cpp
#include <iostream>
#include <map>
#include <vector>
#include <algorithm>
#include <string>
using namespace std;

struct node {
	string name;
	int status, month, time, day, hour, minute;
};

bool cmp(const node &a, const node &b) {
	if (a.name != b.name)
		return a.name < b.name;
	else
		return a.time < b.time;
}

double billFromZero(node call, int *rate) {
	double total = rate[call.hour] * call.minute + rate[24] * 60 * call.day;
	//计算每分钟的费用               +             每天的费用
	for (int i = 0; i < call.hour; i++)
		total += rate[i] * 60;
	//计算每小时的费用
	
	return total / 100.0;
	//转换为正常的费用
}

int main() {
	int rate[25] = { 0 }, n;
	for (int i = 0; i < 24; i++) {
		scanf("%d", &rate[i]);
		rate[24] += rate[i];
	}
	scanf("%d", &n);
	vector<node> data(n);
	for (int i = 0; i < n; i++) {
		cin >> data[i].name;
		scanf("%d:%d:%d:%d", &data[i].month, &data[i].day, &data[i].hour, &data[i].minute);
		string temp;
		cin >> temp;
		data[i].status = (temp == "on-line") ? 1 : 0;
		data[i].time = data[i].day * 24 * 60 + data[i].hour * 60 + data[i].minute;
	}

	sort(data.begin(), data.end(), cmp);
	map<string, vector<node> > custom;
	for (int i = 1; i < n; i++) {
		if (data[i].name == data[i - 1].name&&data[i - 1].status == 1 && data[i].status == 0) {
			custom[data[i - 1].name].push_back(data[i - 1]);
			custom[data[i].name].push_back(data[i]);
		}
	}
	for (auto it : custom) {
		vector<node> temp = it.second;
		cout << it.first;
		printf(" %02d\n", temp[0].month);
		double total = 0.0;
		for (int i = 1; i < temp.size(); i += 2) {
			double t = billFromZero(temp[i], rate) - billFromZero(temp[i - 1], rate);
			//计算这个区间的通话费用
			printf("%02d:%02d:%02d %02d:%02d:%02d %d $%.2f\n", temp[i - 1].day, temp[i - 1].hour, temp[i - 1].minute,
				temp[i].day, temp[i].hour, temp[i].minute,
				temp[i].time - temp[i - 1].time, t
			);
			total += t;
		}
		printf("Total amount: $%.2lf\n", total);
	}
	return 0;
}
```

