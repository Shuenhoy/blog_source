title: kruskal算法
tags: 最小生成树
categories: NOIP
date: "2013-08-12"
---
代码镇楼
```c++
#include "iostream"
#include "vector"
#include "fstream"
#include "algorithm"
using namespace std;
struct Node
{
	int u,v,w;
	bool operator <(const Node &o) const{
		return w<o.w;
	}
};

Node fli[10000];
int father[10000]={0};
int N,M;
int find(int x){
	if(father[x]==x) return x;
	father[x]=find(father[x]);
	return father[x];
}
void Union(int a,int b){
	father[find(a)]=find(father[b]);
}
#define MAX(a,b) (a)<(b)?(b):(a)
int main(int argc, char const *argv[])
{
	//ifstream cin("ff.txt");
	cin>>N>>M;
	for (int i = 1; i <= N; ++i)
		father[i]=i;

	for (int i = 1; i <= M; ++i)
		cin>>fli[i].u>>fli[i].v>>fli[i].w;
	sort(fli,fli+M);
	int ans=0;
	int ingraph=1;
	int i=0;
	while(ingraph<N){
		i++;
		if(find(fli[i].u)!=find(fli[i].v)){
			ingraph++;
			ans=MAX(ans,fli[i].w);
			Union(fli[i].u,find(fli[i].v));
		}
	}
	cout<<N-1<<" "<<ans;
	return 0;
}
```
<!--more-->

题目：https://vijos.org/p/1190


这个最小生成树好像是把图里所有节点连接且权值之和最小的样子吧。

算法好像是把所有路径排序然后找出最小的如果两个不在一个联通分量（用并查集）就添加。

↑  
啊喂哪有这么简单啊

