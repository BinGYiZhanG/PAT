
* 每块输入包含6行：
  * ```Line #1:``` the 7-digit ID number;
  * ```Line #2:``` the book title -- a string of no more than 80 characters;
  * ```Line #3:``` the author -- a string of no more than 80 characters;
  * ```Line #4:``` the key words -- each word is a string of no more than 10 characters without any white space, and the keywords are separated by exactly one space;
  * ```Line #5:``` the publisher -- a string of no more than 80 characters;
  * ```Line #6:``` the published year -- a 4-digit number which is in the range [1000, 3000].
  
  
  ### 处理：
  * ```map<string,set<int> >```,```string```存关键字，```set<int>```存7位ID
  * 对于```key words```的读取，一行之中可能有空格（一行多个关键字，查询时可能只搜索其中一个关键字，所以每个关键字都得记录，也就是分别记录），注意处理
  
  
  ```cpp
  #include <iostream>
#include <cstdio>
#include <map>
#include <set>
#include <string>

using namespace std;

map<string,set<int> > mpTitle,mpAuthor,mpKey,mpPub,mpYear;
void query(map<string,set<int> >& mp,string &str){
    if(mp.find(str)==mp.end())///寻找map的string键：是否在map中
        printf("Not Found\n");
    else{
        for(set<int>::iterator it=mp[str].begin();it!=mp[str].end();it++){///输出7位ID number
            printf("%07d\n",*it);//%7d   和    %07d       是22分，和30分的差距
        }
    }
}

int main(){
    string title,author,key,pub,year;
    int n,m,id,type;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d",&id);
        char c=getchar();
        getline(cin,title);
        mpTitle[title].insert(id);
        getline(cin,author);
        mpAuthor[author].insert(id);
        while(cin>>key){
            mpKey[key].insert(id);
            c=getchar();
            if(c=='\n')
                break;
        }
        getline(cin,pub);
        mpPub[pub].insert(id);
        getline(cin,year);
        mpYear[year].insert(id);
    }
    scanf("%d",&m);
    for(int i=0;i<m;i++){
        string temp;
        scanf("%d: ",&type);
        //cin>>temp;
        getline(cin,temp);
        cout<<type<<": "<<temp<<endl;//这句没写
        if(type==1)
            query(mpTitle,temp);
        else if(type==2)
            query(mpAuthor,temp);
        else if(type==3)
            query(mpKey,temp);
        else if(type==4)
            query(mpPub,temp);
        else
            query(mpYear,temp);
    }
    return 0;
}


  
  ```
  
  
