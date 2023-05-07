---
title: Solution-CF1499D The Number of Pairs【数学】【枚举】【筛素数】
subtitle: Solution-CF1499D The Number of Pairs 有一点点难的数学题。

# Summary for listings and search engines
summary: Solution-CF1499D The Number of Pairs 有一点点难的数学题。

# Link this post with a project
projects: []

# Date published
date: '2021-03-20T08:50:50Z'

# Date updated
lastmod: '2021-03-20T08:50:50Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
# image:
#   caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
#   focal_point: ''
#   placement: 2
#   preview_only: false

authors:
  - admin

tags:
  - Codeforces
  - 解题报告
  - 数学
  - 枚举
  - 筛素数

categories:
  - OI/ACM
  - 解题报告
---

有一点点难的数学题。

> ## Description
>
> You are given three positive (greater than zero) integers $c$, $d$ and $x$.
>
> You have to find the number of pairs of positive integers $(a,b)$ such that equality $\newcommand{\lcm}{\mathrm{lcm}}c\cdot \lcm(a,b)-d\cdot\gcd(a,b)=x$ holds. Where $\lcm(a,b)$ is the least common multiple of $a$ and $b$ and $\gcd(a,b)$ is the greatest common divisor of $a$ and $b$.
>
> ## Input
>
> The first line contains one integer $t (1\le t\le 10^4)$ — the number of test cases.
>
> Each test case consists of one line containing three integer $c$, $d$ and $x$ $(1\le c,d,x\le 10^7)$.
>
> ## Output
>
> For each test case, print one integer — the number of pairs $(a,b)$ such that the above equality holds.
>
> ## Example
>
> **input**
>
> ```
> 4
> 1 1 3
> 4 2 6
> 3 3 7
> 2 7 25
> ```
>
> **output**
>
> ```
> 4
> 3
> 0
> 8
> ```
>
> ## Note
>
> In the first example, the correct pairs are: $(1,4)$, $(4,1)$, $(3,6)$, $(6,3)$.
>
> In the second example, the correct pairs are: $(1,2)$, $(2,1)$, $(3,3)$.

## 题意

给定 $c,d,x(1\le c,d,x\le 10^7)$，求使得 $c\cdot\lcm(a,b)-d\gcd(a,b)=x$ 的有序数对 $(a,b)$ 有多少个。

## 题解

我们知道，$\lcm(a,b)=\frac{ab}{\gcd(a,b)}$。同时，$\frac{a}{\gcd(a,b)},\frac{b}{\gcd(a,b)}$ 都是整数。因此 $\frac{ab}{\gcd(a,b)\gcd(a,b)}$ 是整数。即 $\gcd(a,b)|\lcm(a,b)$。

因此原式 $c\cdot\lcm(a,b)-d\gcd(a,b)=x$ 左边有因子 $\gcd(a,b)$，因此必须有 $\gcd(a,b)|x$。

所以我们枚举 $x$ 的所有因子，作为 $\gcd(a,b)$ 去计算合法的 $(a,b)$ 组数。枚举 $x$ 的因子复杂度为 $\sqrt x$。

此时可求得 $\lcm(a,b)$。$\lcm(a,b)=\frac{x+d\gcd(a,b)}{c}$

有了 $\lcm(a,b)$ 和 $\gcd(a,b)$，我们需要找出有多少对 $(a,b)$。令 $k=\frac{\lcm(a,b)}{\gcd(a,b)}=p_1^{t_1}p_2^{t_2}\cdots p_n^{t_n}$，则每个 $p_i^{t_i}$ 会分配给 $a$ 或 $b$。共有 $2^n$ 种分配方法。

因此求出 $k$ 之后，我们需要将 $k$ 分解质因数。这个的复杂度是 $O(\sqrt k)$ 的，合起来 $O(T\sqrt{kx})$ 比较大。

所以我们可以在筛质数的时候预处理出每个数**有多少个不同的质因子**，统计时直接 $+2^n$ 即可。

另外考虑 $k$ 的范围：
$$
\begin{aligned}
\lcm(a,b)&=\frac{x+d\gcd(a,b)}{c}\\
k=\frac{\lcm(a,b)}{\gcd(a,b)}&=\frac{x}{c\gcd(a,b)}+\frac dc
\end{aligned}
$$
分母均大于等于 $1$，因此 $k\le x+d\le 2\times 10^7$。

时间复杂度 $O(\max\{c,d,x\}+T\sqrt x)$。

鸣谢 Dew。

## Code：

```cpp
#include<unordered_map>
#include<queue>
#include<cstdio>
#include<cstring>
#include<algorithm>
#include<iostream>
#define ll long long
#ifdef wjyyy
    #define gc getchar
#else
    #define gc() (p1==p2&&(p2=(p1=buf)+fread(buf,1,1<<21,stdin),p1==p2)?EOF:*p1++)
#endif
char buf[2100000],*p1=buf,*p2=buf;
using namespace std;
ll Abs(ll x)
{
	return x>0?x:-x;
}
ll read()
{
    ll x=0,f=1;
    char ch=gc();
    while(ch<'0'||ch>'9')
    {
    	if(ch=='-')
    		f=-1;
    	ch=gc();
	}
    while(ch>='0'&&ch<='9')
    {
        x=x*10+(ch&15);
        ch=gc();
    }
    return x*f;
}
int pri[2000000],cnt=0,p[20000001];
//pri表示质数列 pi表示i的最小质因子
ll num[20000001];
//numi表示i有多少个不同的质因子
bool is[20000001];
//是否是非质数
ll ans=0,c,d,k;
void work(ll i)
{
	if((k+d*i)%c)//求出lcm
		return;
	ll lcm=(k+d*i)/c;
	if(lcm%i)
		return;
	ll t=lcm/i;
	ans+=1<<num[t];
}
int main()
{
	is[0]=1;
	is[1]=1;
	for(int i=2;i<=20000000;++i)
	{
		if(!is[i])//如果是质数
		{
			pri[++cnt]=i;
			num[i]=1;//它的质因子只有一个
			p[i]=i;//它的最小质因子是它自己
		}
		for(int j=1;j<=cnt&&pri[j]*i<=20000000&&pri[j]<=p[i];++j)
		{
			int q=pri[j]*i;
			is[q]=1;
			num[q]=num[i]+(i%pri[j]!=0);//判断是否新增质因子
			p[q]=pri[j];
		}
	}
	int T=read();
	while(T--)
	{
		ans=0;
		c=read();
		d=read();
		k=read();
		for(int i=1;i*i<=k;++i)
			if(k%i==0)
			{
				work(i);
				if(i*i!=k)
					work(k/i);
			}
		printf("%lld\n",ans);
	 } 
	return 0;
}
```


