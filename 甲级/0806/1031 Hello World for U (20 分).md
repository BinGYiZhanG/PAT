不知道如何得到的```n1,n2,n3```
学习点：
* 输出，值得学习

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <cmath>
using namespace std;

int main() {
	int n1, n2, n3, n;
	string s;
	cin >> s;
	n = s.size();
	n1 = n3 = (n + 2) / 3;
	n2 = n - n1 * 2;
	for (int i = 0; i < n1 - 1; i++) {
		cout << s[i];
		for (int j = 0; j <= n2 - 1; j++)
			cout << " ";
		cout << s[n - i - 1] << endl;
	}
	for (int i = n1-1; i <= n1+n2; i++) {
		cout << s[i];
	}
	return 0;
}

```

