title: 摆花问题存档
tags: 动态规划
categories: NOIP
date: "2013-08-07"
---


### 代码

```c++
#include "iostream"
using namespace std;
int n;
int m;
int f[1001][1001]={0};
int a[1001]={0};
int main()
{

	cin>>n>>m;
	for(int i=1;i<=n;i++)  cin>>a[i];
	for (int i = 0; i <= a[1]; ++i)	f[1][i]=1;
	for (int i = 2; i <= n; ++i){
		f[i][0]=1;
		for (int j = 1; j <= m; ++j)
			for (int k = 0; k <= a[i]; ++k)
				if(j-k>=0)
					f[i][j]=(f[i][j]+f[i-1][j-k])%1000007;
	}
	
	cout<<f[n][m]<<endl;
	system("pause");
	return 0;
}
```

### 分析
f\[i][j]代表将i种花放在j个花瓶中的最大方案数

	f[i][j]={ 1 若j=0(即无空间） 或 i=0 且 0<=j<=a[1] (即只有一种花）  
    	    { Σ f[i-1][j-k] 选择k中花的情况之和
