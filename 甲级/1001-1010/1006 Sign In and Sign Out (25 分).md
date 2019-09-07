
### 题目大意：
* 给出n个人的id、sign in时间、sign out时间，求最早进来的人和最早出去的人的ID～

#### 还是对时间处理一下比较好（把时间变成可以直接比较大小的整形对象）
```c++ 
#include <bits/stdc++.h>

using namespace std;

string minstr,maxstr;
string tmpstr;
int minin=86400,maxout=0;
int tmpin,tmpout;
int hh1,mm1,ss1,hh2,mm2,ss2;

int main(){
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        cin>>tmpstr;
        scanf("%d:%d:%d %d:%d:%d",&hh1,&mm1,&ss1,&hh2,&mm2,&ss2);
        //cout<<tmpstr<<" "<<hh1<<" "<<mm1<<" "<<ss1<<" "<<hh2<<" "<<mm2<<" "<<ss2<<endl;
        int signin=hh1*3600+mm1*60+ss1;
        int signout=hh2*3600+mm1*60+ss2;
        if(signin<minin){
            minin=signin;
            minstr=tmpstr;
        }
        if(signout>maxout){
            maxout=signout;
            maxstr=tmpstr;
        }
    }
    cout<<minstr<<" "<<maxstr<<endl;
    return 0;
}





/*
#include <iostream>
#include <string>

using namespace std;

int main()
{
	int n;
	cin >> n;
	if (n == 0) {
		cout << endl;
		return 0;
	}
	string min, max, str;
	int min1, min2, min3, max1, max2, max3;
	cin >> str;
	min = str;
	max = str;
	scanf("%d:%d:%d %d:%d:%d", &min1, &min2, &min3, &max1, &max2, &max3);

	for (int i = 1; i < n; i++) {
		cin >> str;
		int a1, a2, a3, b1, b2, b3;
		scanf("%d:%d:%d %d:%d:%d",&a1,&a2,&a3,&b1,&b2,&b3);
		if ((a1 < min1) || ((a1 == min1) && (a2 < min2)) || ((a1 == min1) && (a2 == min2) && (a3 < min3))) {
			min = str;
			min1 = a1;
			min2 = a2;
			min3 = a3;
		}
		if ((b1 > max1) || ((b1 == max1) && (b2 > max2)) || ((b1 == max1) && (b2 == max2) && (b3 > max3))) {
			max = str;
			max1 = b1;
			max2 = b2;
			max3 = b3;
		}
	}
	cout << min << " " << max;
	return 0;
}
*/
```
