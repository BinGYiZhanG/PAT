给出一个至多含M个元素的栈。将N个元素按1,2,3...的顺序推入，并且随机推出。你应该告诉一个被给的数字序列是否是栈的pop序列。例如，如果M是5，N是7，可以从栈中推得1,2,3,4,5,6,7是
，但是不能获得3,2,1,7,5,6,4。<br>

### 输入:
M，栈的最大容量；N，push序列的长度；K，需要检查的pop序列的数目。<br>
接下来K行，每行包含一个含有N个数的pop序列。<br>

### 输出：
输出“YES”或者“NO”。

### 关键模拟

```cpp
#include <iostream>
#include <cstdio>
#include <stack>

using namespace std;

const int maxn=1010;
int s[maxn];
int m,n,k;


int main(){
    stack<int> st;
    scanf("%d%d%d",&m,&n,&k);
    while(k--){
        while(!st.empty())
            st.pop();

        for(int i=1;i<=n;i++){
            scanf("%d",&s[i]);
        }

        bool flag=true;
        int cur=1;
        for(int i=1;i<=n;i++){
            st.push(i);

            if((int)st.size()>m){
                flag=false;
                break;
            }
            while(!st.empty()&&st.top()==s[cur])
            {
                cur++;
                st.pop();
            }
        }

        if(flag&&st.empty())
            printf("YES\n");
        else
            printf("NO\n");
    }
}


```

