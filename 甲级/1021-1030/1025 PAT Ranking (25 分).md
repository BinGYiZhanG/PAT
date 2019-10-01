

* 问题：
  * 对于单独考场排序，和总排序问题
    * 在读取数据的时候就分考场读，并且读完就处理单独考场的考生分排名
    * 最后总排序，就是读完总的数据之后再排序


```cpp
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>
using namespace std;

const int maxn = 30100;
struct person {
	string num;
	int scr;
	int finalrank;
	int localnumber;
	int localrank;
}per[maxn];

//准考证号排序
bool cmp(person a, person b) {
	if (a.scr != b.scr)
		return a.scr > b.scr;
	else
		return a.num < b.num;
}

int main() {
	int n;
	cin >> n;
	int tmp=0;
	for (int i = 1; i <= n; i++) {
		int k;
		cin >> k;
		for (int j = 0; j < k; j++) {
			cin >> per[tmp + j].num >> per[tmp + j].scr;
			per[tmp + j].localnumber = i;
		}
		//这步操作牛！！！！！！！！！
		sort(per + tmp, per + tmp + k, cmp);
		per[tmp].localrank = 1;
		//j=tmp+1
		for (int j = tmp+1; j <tmp + k; j++) {
			if (per[j].scr != per[j - 1].scr)
				per[j].localrank = j - tmp + 1;//输出对应的当前名次，肯定不能是第1，
			else
				per[j].localrank = per[j - 1].localrank;
		}
		tmp += k;
	}
	sort(per, per + tmp, cmp);
	/*for (int i = 0; i < tmp; i++) {
		cout << per[i].num << " " <<per[i].localrank<<" "<< per[i].scr << endl;
	}*/
	per[0].finalrank = 1;
	for (int i = 1; i < tmp; i++) {
		if (per[i].scr != per[i - 1].scr)
			per[i].finalrank = i + 1;//输出对应的当前名次，肯定不能是第1，
		else
			per[i].finalrank = per[i - 1].finalrank;
	}
	cout << tmp << endl;
	for (int i = 0; i < tmp; i++) {
		cout << per[i].num << " " << per[i].finalrank<<" "<<per[i].localnumber << " " << per[i].localrank << endl;
	}
	return 0;
}


```
