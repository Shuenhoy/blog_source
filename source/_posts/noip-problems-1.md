title: 1道NOIP题-开心的金明
categories: noip
date: 2013-05-01 14:07:05
tags: 背包问题 
---

以后每个周都要做NOIP题或者在这里记录,先放1道 开心的金明

**注意!这里纯粹是我自己记录的,被误导了概不负责**

<!--more-->

### 开心的金明

题目描述:
  >金明今天很开心，家里购置的新房就要领钥匙了，新房里有一间他自己专用的很宽敞的房间。
  >更让他高兴的是，妈妈昨天对他说：“你的房间需要购买哪些物品，怎么布置，你说了算，只要不超过N 元钱就行”。
  >今天一早金明就开始做预算，但是他想买的东西太多了，肯定会超过妈妈限定的N 元。
  >于是，他把每件物品规定了一个重要度，分为5 等：用整数1~5 表示，第5 等最重要。
  >他还从因特网上查到了每件物品的价格（都是整数元）。他希望在不超过N 元（可以等于N 元）的前提下，
  >使每件物品的价格与重要度的乘积的总和最大。设第j 件物品的价格为v[j]，重要度为w[j]，共选中了k 件物品，
  >编号依次为j1...jk，则所求的总和为：v[j1]*w[j1]+..+v[jk]*w[jk]请你帮助金明设计一个满足要求的购物单.
  
  >**输入格式**

  >输入的第1 行，为两个正整数，用一个空格隔开：
  >N m
  >（其中N（<30000）表示总钱数，m(<25)为希望购买物品的个数。） 
  >从第2 行到第m+1 行，第j 行给出了编号为j-1的物品的基本数据，
  >每行有2 个非负整数v p（其中v 表示该物品的价格（v≤10000），p 表示该物品的重要度（1~5））
  
  >**输出格式**

  >输出只有一个正整数，为不超过总钱数的物品的价格与重要度乘积的总和的
  >最大值（<100000000）
  

据说这是一个叫做0/1背包问题的诡异玩意

也就是说有一大堆东西,每个都有一定的价值和重量,同时你有一个有限容量的包,要求是使价值最大.在这里价值就是重要度\*价格,重量就是价格,容量就是总钱数

现在所有所有的物品的重量和价值分别被仍在了P和I两个数组中,我们设W(n,N)表示将数组的0到n这些物品放入容量为N的最大收益,我们可以知道如果N<=0,即这些没法装,这是W(n,N)=0

如果N>0,就是可以装的下,分为两种情况,就是装第n个或不装.装的时候就是就是第n的价格加上到第n-1个物品扔到N-第n个的重量,即W1=P[n]+(n,N-V[n]),否则是不装,W2=W(n,N),两者中大的即是结果

说了一大堆发现我说不太明白,上代码吧= =

```c++
#include<cstdio>
#include<algorithm>
#include<functional>
#include<iostream>

using namespace std;
const int MAX=25;
inline int Max(int a,int b){
    return a>b?a:b;
}

int m;

int P[MAX]={0}; // 价值 

int V[MAX]={0}; 
int C[MAX][30000]={ { -1, -1 } };
int work(int n,int N){
    if(n==0 || N<=0){
        C[n][N]=0;
        return 0;
    }
    if(C[n][N]!=-1){
        
        return C[n][N];
    }
    int i=n-1;
    if(V[i]>N){
        C[n][N]= work(i,N);
    } else {
        int tmp1=work(i,N);
        
        int tmp2=P[i]+work(i,N-V[i]);
        
        C[n][N]= Max(tmp1,tmp2);
    }
    return C[n][N];
    
    
}
int main(){
    int N;
   
    scanf("%d %d",&N,&m);
    
    
    
    for(int i =0;i<m;i++){
        
        scanf("%d %d",V+i,P+i);

        P[i]*=V[i];
    }
    for(int i=0;i<=m;i++){
        for(int j=0;j<=N;j++){
            C[i][j]=-1;
        }
    }
    printf("%d\n",work(m,N));
    system("pause");
    return 0;   
}


```