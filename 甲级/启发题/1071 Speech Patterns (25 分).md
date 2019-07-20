输入：
以'\n'符作为结束, 每一个字符都在[0-9 A-Z a-z].
输出：
打印在输入文本中最常出现的单词，如果单词不止一个，则按字典序进行打印,打印全为小写,单词的大小写不敏感。

### map基本用法
```cpp

#include <iostream>
#include <cstdio>
#include <string>
#include <map>

using namespace std;

bool check(char c){
  if(c>='0'&&c<='9')
  return true;
  if(c>='a'&&c<='z')
  return true;
  if(c>='A'&&c<='Z')
  return true;
  return false;
}
int main(){
  map<string,int> count_;
  string str;
  getline(cin,str);
  int i=0;
  while(i<str.size()){
    string word;
    while(i<str.size()&&check(str[i])){
      if(str[i]>='A'&&str[i]<='Z')
        str[i]+=32;
      word+=str[i];
      i++;
    }
    if(word!=""){
      if(count_.find(word)==count_.end()){
        count_[word]=1;
      }
      else
        count_[word]++;
    }
    while(i<str.size()&&!check(str[i])){
      i++;
    }
  }
  int MAX=0;
  string ans;
  for(map<string,int>::iterator it=count_.begin();it!=count_.end();it++){
    if(MAX<it->second){
      MAX=it->second;
      ans=it->first;
    }
  }
  cout<<ans<<" "<<MAX<<endl;
  return 0;
}

```
