title: SPFA
tags: 最短路
categories: NOIP
date: "2013-08-12"
---

今天写某道难度1的最短路问题(https://vijos.org/p/1635)，然后一开始用Dijkstra写写了半天发现一直很奇葩的只输出0= =于是一怒之下竟然删掉了代码重新用SPFA写。

SPFA就是要用一个队列，一开始起点放在队列里，如果队列空了就说明寻路完毕。然后不断取出队首元素，遍历与其相邻的结点，如果从对首结点到遍历到的结点距离之和加起来比遍历到的结点本身的距离小就替换。

p.s.自我感觉SPFA比Dijkstra要好理解到现在我也没弄明白Dijkstara是怎么回事= =

然后发现输出还是0 = = == = = = =

于是折腾了半个下午，最后发现原来竟然是输出的时候输出了N而不是N-1所以输出了0.

然后满心欢喜的去提交了测试，然后奇葩的发现不是超时就是错误啊啊啊啊

程序附上求好心人解答：
```c++

#include "iostream"
#include "list"
#include "fstream"
#include "queue"
#include "climits"
using namespace std;
struct Node
{
	int u,v,c;
};
list<Node> fklist[10000];
int N;
unsigned int D[100000]={0};
queue<int> q;
bool inq[100000]={false};
int prev[100000]={0};
int main(int argc, char const *argv[])
{
	scanf("%d",&N);
	for (int i = 0; i < N; ++i){
		for (int j = 0; j < N; ++j)
		{
			int a;
			scanf("%d",&a);
			if(a!=0){
				fklist[i].push_back((Node){i,j,a});
				fklist[j].push_back((Node){j,i,a});
			}
		}
		D[i]=INT_MAX;
		prev[i]=-1;
	}
	
	D[0]=0;
	q.push(0);
	while(!q.empty()){
		int u=q.front();q.pop();inq[u]=false;
		for (std::list<Node>::iterator i = fklist[u].begin(); i != fklist[u].end(); ++i){
			if(D[(*i).v]>D[u]+(*i).c){
				D[(*i).v]=D[u]+(*i).c;
				prev[(*i).v]=u;
				if(!inq[(*i).v]){
					q.push((*i).v);
					inq[(*i).v]=true;
				}
			}
			
		}
	}
	int out[10000]={0};
	int j=0;
	for(int i=N-1;i!=-1;i=prev[i],j++) out[j]=i+1;
	for(int i=j-1;i>=0;i--) cout<<out[i]<<" ";
	cout<<endl<<D[N-1]<<endl;
	return 0;
}

```
