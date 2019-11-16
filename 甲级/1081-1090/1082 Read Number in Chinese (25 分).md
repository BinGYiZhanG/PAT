

### 题意:
* 将数字以汉字形式输出


* 我只会简单模拟，并且还没模拟完（最后的情况太多）
```
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <vector>
#include <string>

using namespace std;

string num[11] = {"ling ","yi ","er ","san ","si ","wu ","liu ","qi ","ba ","jiu "};
string book[6] = {"","Shi ","Bai ","Qian ","Wan ","Yi "};

int main(){
    string number;
    cin>>number;
    if(number[0]=='-'){
        printf("Fu");
        number.erase(number.begin());
    }
    if(number.size()<4){///最高位是百位
        if(number.size()==1){///一位
            cout<<num[number[0]-'0']<<endl;
        }
        if(number.size()==2){
            int shi = number[0] - '0';
            int ge = number[1] - '0';
            cout<<num[shi]<<book[1]<<num[ge]<<endl;
        }
        if(number.size()==3){
            int bai = number[0] - '0';
            int shi = number[1] - '0';
            int ge = number[2] - '0';

            if(shi==0&&ge==0){
                cout<<num[bai]<<book[2]<<endl;
            }
            else if(shi==0&&ge!=0){
                cout<<num[bai]<<book[2]<<num[shi]<<num[ge]<<endl;
            }
            else if(shi!=0&&ge==0){
                cout<<num[bai]<<book[2]<<num[shi]<<book[1]<<endl;
            }
            else
                cout<<num[bai]<<book[2]<<num[shi]<<book[1]<<num[ge]<<endl;
        }
    }
    else if(number.size()<7){
        if(number.size()==4){///只有4位的时候，
            int qian = number[0] - '0';
            int bai = number[1] - '0';
            int shi = number[2] - '0';
            int ge = number[3] - '0';

            if(!ge&&!shi&&!bai)///7000
                cout<<num[qian]<<book[3]<<endl;
            else if(!ge&&!shi)///7700
                cout<<num[qian]<<book[3]<<num[bai]<<book[2]<<endl;
            else if(!ge&&!bai)///7080
                cout<<num[qian]<<book[3]<<num[bai]<<book[1]<<endl;
            else if(!shi&&!bai)///8008
                cout<<num[qian]<<book[3]<<num[bai]<<num[ge]<<endl;
            else
                cout<<num[qian]<<book[3]<<num[bai]<<book[2]<<num[shi]<<book[1]<<num[ge]<<endl;
        }
        
        if(number.size()==5){
            
        }
        
    }


    return 0;
}


```


* 带注释的题解

```
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>
using namespace std;

char num[10][5] = {
	"ling","yi","er","san","si","wu","liu","qi","ba","jiu"
};
///                  0     1     2     3     4
char wei[5][5] = { "Shi","Bai","Qian","Wan","Yi" };
int main() {
	string str;
	cin >> str;
	int len = str.length();
	int left = 0, right = len - 1;///right 指向 数字字符串 的最后一位 ,left 指向 数字字符串 的第一位
	if (str[0] == '-') {///输出负号
		printf("Fu");
		left++;
	}
	while (left + 4 <= right) {///从高位向右开始处理（每4位处理）,
		right -= 4;
	}
	while (left < len) {
		bool flag = false;
		bool isPrint = false;
		while (left <= right) {
        /*
            102489602
            1 亿 零 2 百 4 十 8 万 9 千 6 百 零 2

            120489602
            1 亿 2 千 零 4 十 8 万 9 千 6 百 零 2

        */
			if (left > 0 && str[left] == '0')///当遇到0时，读汉字数时要读出ling来，
				flag = true;
			else {
				if (flag == true) {///当遇到0时，读汉字数时要读出ling来，
					printf(" ling");
					flag = false;
				}
				if (left > 0)//判断特例:0的情况,输出ling
					printf(" ");
				printf("%s", num[str[left] - '0']);///
				isPrint = true;
				if (left != right) {///输出 单位（千，百，十 三者中取）
					printf(" %s", wei[right - left - 1]);
				}
			}
			left++;
		}
		if (isPrint&&right != len - 1) {///相当于输出亿 , 万 , 千 三者中取
			printf(" %s", wei[(len - 1 - right) / 4 + 2]);
		}
		right += 4;
	}
	return 0;
}


```


