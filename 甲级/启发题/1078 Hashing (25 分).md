这个问题的任务很简单：向一个哈希表里插入一个独一无二的正数序列，并且输出输入数字的位置。哈希函数被定义为 H(key)=key%TSize,TSize是哈希表的最大容量，二次探测(仅带正增量)用于解决冲突问题。<br>
需要指出表的大小是素数，如果所给大小不是素数，你应该重新定义表的大小以一个大于所给表大小的最小素数，<br>

输入：

MSize，定义表的大小；N，所给数字个数。

输出：
打印每个数字相应的位置，如果无法插入元素，打印“-”。

![](https://github.com/BinGYiZhanG/PAT/blob/master/Images/07181059.png)

未A代码<br>
可能是加了一个table数组导致错误
```cpp
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <cmath>
using namespace std;

bool is_prime(int n){
    if(n<=1)    return false;
    int sqr=(int)sqrt(n);
    for(int i=2;i<=sqr;i++){
        if(n%i==0)
            return false;
    }
    return true;
}

int table[31111];
int a[31111];
bool vis[31111];
int main(){
    int MSize,N;
    scanf("%d%d",&MSize,&N);
    for(int i=0;i<N;i++){
        scanf("%d",a+i);
    }
    while(!is_prime(MSize)){
        MSize++;
    }

    for(int i=0;i<N;i++){
        int tmpos=a[i]%MSize;
        if(vis[tmpos]==false){///没有发生冲突
            table[a[i]]=tmpos;
            vis[tmpos]=true;
        }
        else{///发生冲突
            int flag=0;
            for(int j=1;j<30010;j++){
                tmpos=(a[i]+j*j)%MSize;
                if(vis[tmpos]==false){///没有发生冲突
                    table[a[i]]=tmpos;
                    vis[tmpos]=true;
                    flag=1;
                }
            }
            if(flag==0)
                table[a[i]]=-1;
        }
    }
    for(int i=0;i<N;i++){
        if(i!=0)
            printf(" ");
        if(table[a[i]]==-1)
            printf("-");
        else
            printf("%d",table[a[i]]);
    }
    return 0;
}

```



