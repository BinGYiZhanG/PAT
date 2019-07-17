```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
using namespace std;

typedef long long ll;

struct Fraction{
  ll up,down;
}a,b;

ll gcd(ll a,ll b){
//ll gcd(ll a, llb){
    return b==0?a:gcd(b,a%b);
//  return a==0?b=0:gcd(b,a%b);
}

Fraction reduction(Fraction result){
  if(result.down<0){
//  if(result.up<0){
    result.up=-result.up;
    result.down=-result.down;
  }
  if(result.up==0)
    result.down=1;
  else{
    int a=gcd(abs(result.up),abs(result.down));
    result.up/=a;
    result.down/=a;
  }
  return result;
}

Fraction add(Fraction f1,Fraction f2){
  Fraction result;
  result.up=f1.up*f2.down+f2.up*f1.down;
  result.down=f1.down*f2.down;
//  reduction(result);
//  return result;
  return reduction(result);
}

Fraction minu(Fraction f1,Fraction f2){
  Fraction result;
  result.up=f1.up*f2.down-f2.up*f1.down;
  result.down=f1.down*f2.down;
//  reduction(result);
//  return result;
  return reduction(result);
}

Fraction multi(Fraction f1,Fraction f2){
  Fraction result;
  result.up=f1.up*f2.up;
  result.down=f1.down*f2.down;
//  reduction(result);
//  return result;
  return reduction(result);
}

Fraction dividen(Fraction f1,Fraction f2){
  Fraction result;
  result.up=f1.up*f2.down;
  result.down=f1.down*f2.up;
//  reduction(result);
//  return result;
  return reduction(result);
}

void showResult(Fraction result){
  result=reduction(result);//这句没加
  if(result.up<0)
    printf("(");
//  if(result.up==0){
//    printf("0");
//  }
  if(result.down==1){
    printf("%lld",result.up);
  }
  else if(abs(result.up)>result.down){
    printf("%lld %lld/%lld",result.up/result.down,abs(result.up)%result.down,result.down);//0分与15分的差距
  //printf("%lld %lld/%lld",result.up/result.down,result.up%result.down,result.down);
  }
  else{
    printf("%lld/%lld",result.up,result.down);
    //注意是 "/"
  }
/*
  if(result.up<result.down)//真分数
    printf("%lld %lld\n",result.up,result.down);
  else{//假分数
    printf("%lld %lld/%lld\n",result.up/result.down,result.up%result.down,result.down);
  }
  */
  if(result.up<0)
    printf(")");
}

int main(){
 // Fraction a,b;
  scanf("%lld/%lld %lld/%lld",&a.up,&a.down,&b.up,&b.down);
  showResult(a); printf(" + "); showResult(b); printf(" = "); showResult(add(a,b));printf("\n");
  showResult(a); printf(" - "); showResult(b); printf(" = "); showResult(minu(a,b));printf("\n");
  showResult(a); printf(" * "); showResult(b); printf(" = "); showResult(multi(a,b));printf("\n");
//  showResult(a); printf(" / "); showResult(b); printf(" = "); showResult(dividen(a,b));
  showResult(a); printf(" / "); showResult(b); printf(" = "); if(b.up==0)	printf("Inf"); else showResult(dividen(a,b));
                                                                        //printf("inf");//导致15分
  return 0;
}

```
