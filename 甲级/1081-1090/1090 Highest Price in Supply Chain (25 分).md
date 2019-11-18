
### 题意:
* 现在给出一条供应链，你应该告诉我们能够从一些供应商那里获得的最高价格

### 输入：
* 第一行，N，供应链上成员总个数；P，根供应者的价格；r，从每个分发者到供应商增加的价格率
* 第二行，-1代表是跟供应商，each number Si is the index of the supplier for the i-th member

### 输出：
* 输出两个参数：
  * 1,我们期望从一些零售商那里获得最高价格，保留两位小数
  * 2,销售最高价格的零售商数目

### 思路：
* 找树的最深层数，和树的最深层数的叶子节点数

我的解法，也对
```cpp

const int maxn=100010;

int n;
double p,r;
int book[maxn];
vector<int> node[maxn];
int maxlevel=0;

void DFS(int index,int level){
    book[level]++;
    if(maxlevel<level)
        maxlevel=level;
    for(int i=0;i<(int)node[index].size();i++)
        DFS(node[index][i],level+1);
}

int main(){
    cin>>n>>p>>r;
    int root=0;
    for(int i=0;i<n;i++){
        int tmp;
        scanf("%d",&tmp);
        if(tmp==-1)
            root=i;
        else
            node[tmp].push_back(i);
    }
    memset(book,0,sizeof(book));
    DFS(root,0);
    printf("%.2f %d\n",p*pow(1+r/100,maxlevel),book[maxlevel]);
    return 0;
}

```

```cpp
const int maxn = 100010;
vector<int> child[maxn];
double p, r;

int num = 0, maxDepth = 0, n;
void DFS(int index, int depth) {
	if (child[index].size() == 0) {
		if (depth > maxDepth) {
			maxDepth = depth;
			num = 1;
		}
		else if (depth == maxDepth) {
			num++;
		}
		return;
	}
	for (int i = 0; i < child[index].size(); i++) {
		DFS(child[index][i], depth + 1);
	}
	
}

int main() {
	int father, root;
	scanf("%d%lf%lf", &n, &p, &r);
	r /= 100;
	for (int i = 0; i < n; i++) {
		scanf("%d", &father);
		if (father != -1) {
			child[father].push_back(i);
		}
		else {
			root = i;
		}
	}
	DFS(root, 0);
	printf("%.2f %d\n", p*pow(1 + r, maxDepth), num);
	return 0;
}
```
