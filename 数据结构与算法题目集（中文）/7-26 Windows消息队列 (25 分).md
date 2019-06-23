### 优先队列

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <queue>
using namespace std;

struct Node{
	string cmd;
	int rank;
	friend bool operator <(Node a,Node b){
		return a.rank>b.rank;
	}
}node;

bool cmp(Node a,Node b){
	return a.rank<b.rank;
}
priority_queue<Node> pq;

int main(){
	int n;
	string cmd1,cmd2;
	int cmd3;
	scanf("%d",&n);
	for(int i=0;i<n;i++){
		cin>>cmd1;
		if(cmd1=="PUT"){
			cin>>cmd2;
			scanf("%d",&cmd3);
			node.cmd=cmd2;
			node.rank=cmd3;
			pq.push(node);
		}
		else{
			if(pq.size()==0)
				printf("EMPTY QUEUE!\n");
			else{
				Node a=pq.top();
				pq.pop();
				cout<<a.cmd<<endl;
			}
		}
	}
	return 0;
}
```

