### 看到队列题，就慌。。。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
struct node {
	int come, time;
}tempcustomer;

bool cmp(node a, node b) {
	return a.come < b.come;
}

int main() {
	int n, k;
	scanf("%d%d", &n, &k);
	vector<node> custom;
	for (int i = 0; i < n; i++) {
		int hh, mm, ss, time;
		scanf("%d:%d:%d %d", &hh, &mm, &ss, &time);
		int cometime = hh * 3600 + mm * 60 + ss;
		if (cometime > 61200)//超出17时
			continue;
		//		tempcustomer = { cometime,time * 60 };
		custom.push_back({ cometime,time * 60 });
	}
	sort(custom.begin(), custom.end(),cmp);
	vector<int> window(k, 28800);//表示某个窗口的结束时间,初始化为28800表示8点开门

	double result = 0.0;
	for (int i = 0; i < custom.size(); i++) {
		int tempindex = 0, minfinish = window[0];
		for (int j = 1; j < k; j++) {
			if (minfinish > window[j]) {
				//选择最早结束的窗口
				minfinish = window[j];
				tempindex = j;
			}
		}
		if (window[tempindex] <= custom[i].come) {
			//如果最早结束时间比他还早，那么他一来就能被服务，更新window的值
			window[tempindex] = custom[i].come + custom[i].time;
		}
		else {
			//如果最早结束时间比他晚，他需要等待，累加等待的时间，然后更新window的值
			result += (window[tempindex] - custom[i].come);
			window[tempindex] += custom[i].time;
		}
	}
	if (custom.size() == 0)
		printf("0.0");
	else
		printf("%.1f", result / 60.0 / custom.size());
	return 0;

}
```
