### 题意：
* Given a stack which can keep M numbers at most. Push N numbers in the order of 1, 2, 3, ..., N and pop randomly. You are supposed to tell if a given sequence of numbers is a possible pop sequence of the stack.

### 思路：
* 我的代码有问题，读入一组数据就死机了

```
#include <iostream>
#include <stack>
#include <cstdio>
#include <vector>

using namespace std;

const int maxn=1010;
int vec[maxn];

int main(){
    int M,N,K;
    bool flag;
    int cur;
    scanf("%d%d%d",&M,&N,&K);
    for(int i=0;i<K;i++){
        stack<int> st;
        flag=true;
        cur=1;
        //vector<int> vec(N+1);
        for(int i=1;i<=N;i++)
            scanf("%d",&vec[i]);

        for(int i=1;i<=N;i++){
            st.push(i);

            if((int)st.size()>M){
                flag=false;
                break;
            }

            while(st.top()==vec[cur]&&!st.empty()){
                st.pop();
                cur++;
            }

        }
        if(flag&&st.empty())
            printf("YES\n");
        else
            printf("NO\n");

    }
}

```
