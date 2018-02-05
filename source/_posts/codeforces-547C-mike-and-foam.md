---
title: Codeforces 547C Mike and Foam Tutorial
date: 2018-02-05 15:45:30
tags: mobius inclusion-exclusion-principle
---

# Problem Description

Given n elements and m add and delete queries, you are to output the number of coprime pairs after each query.

# Analysis

Note that we can use answers to the previous query to answer the current query. We only need to add/subtract the number of coprime numbers to/from the previous answer.

For example, when given a number 6, we need to find how many numbers are coprime to 6. Let f(x) be the number of integers that are multiples of x, and with the inclusion-exclusion principle, we can write the number of coprimes of 6 as f(1)-f(2)-f(3)+f(6).

Observing the above formula, we can find out that the coefficients satisfy the mobius function, and we can speed up the algorithm by using it.

To calculate the mobius function values, we can let mobius(1)=1, and subtract it from mobius(i * j) for j>1.

# Code

```C++
#include <stdio.h>
#include <vector>
using namespace std;
bool npr[500001],inshelf[200001],has[500001];
int mobius[500001],cntp,a[200001],cnt[500001];
vector<int> fac[500001];
int main()
{
	int n,q;
	scanf("%d%d",&n,&q);
	for (int i=1;i<=n;++i)
	{
		scanf("%d",a+i);
		has[a[i]]=1;
	}
	for (int i=1;i<=500000;++i)
	{
		if (i==1)
			mobius[i]=1;
		for (int j=i;j<=500000;j+=i)
		{
			if (has[j])
				fac[j].push_back(i);
			if (i!=j)
				mobius[j]-=mobius[i];
		}
	}
	long long ans=0;
	for (int i=1;i<=q;++i)
	{
		int x;
		scanf("%d",&x);
		inshelf[x]^=1;
		if (inshelf[x])
			for (int j:fac[a[x]])
				ans+=mobius[j]*(cnt[j]++);
		else
			for (int j:fac[a[x]])
				ans-=mobius[j]*(--cnt[j]);
		printf("%lld\n",ans);
	}
	return 0;
}
```
