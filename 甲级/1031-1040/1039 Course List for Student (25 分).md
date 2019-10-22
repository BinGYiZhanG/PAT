**坑**:直接用map插入是不可以的，会超时

* 运行超时代码:
```cpp
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>
#include <map>
#include <set>

using namespace std;

map<string,set<int> > mp;

int main(){
    int n,k;
    scanf("%d%d",&n,&k);
    for(int i=0;i<k;i++){
        int course,x;
        scanf("%d%d",&course,&x);
        for(int j=0;j<x;j++){
            string str;
            cin>>str;
            mp[str].insert(course);
        }
    }
    for(int i=0;i<n;i++){
        string str;
        cin>>str;
        cout<<str;
        printf(" %d",mp[str].size());
        for(set<int>::iterator it=mp[str].begin();it!=mp[str].end();it++){
            printf(" %d",*it);
        }
        printf("\n");
    }
    return 0;
}

```

方法:name数组转成ID，然后进行存储，

```cpp


#include <iostream>
#include <cstring>
#include <vector>
#include <cstdio>
#include <algorithm>
using namespace std;
const int N=40010;
const int M=26*26*26*10+1;
vector<int> selectCourse[M];

int getID(char name[]){
    int ID=0;
    for(int i=0;i<3;i++){
        ID=ID*26+(name[i]-'A');
    }
    ID=ID*10+name[3]-'0';
    return ID;
}

int main(){
    int N,K;
    char name[5];
    scanf("%d%d",&N,&K);
    for(int i=0;i<K;i++){
        int course,x;
        scanf("%d%d",&course,&x);
        for(int j=0;j<x;j++){
            scanf("%s",name);
            int ID=getID(name);
            selectCourse[ID].push_back(course);
        }
    }
    for(int i=0;i<N;i++){
        scanf("%s",name);
        int ID=getID(name);
        //sort函数不会用了,写成数组形式了,首地址，到尾地址
        sort(selectCourse[ID].begin(),selectCourse[ID].end());
        printf("%s %d",name,selectCourse[ID].size());
        for(int j=0;j<selectCourse[ID].size();j++){
            printf(" %d",selectCourse[ID][j]);
        }
        printf("\n");
    }
    return 0;
}

```


