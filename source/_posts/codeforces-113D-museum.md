---
title: Problem Description - 1
date: 2018-2-4 20:21:07
tags: Problem Description
---

# Problem Description

There is an undirected graph consisting of n vertices and m edges. Initially, two persons are at vertices a and b, respectively. In one step where they are not in the same room, each person has probability pi of staying at his original position. If not, he moves to an adjacant vertex with equal probability. Output the probabilities for them to meet at each room. n<=22, m<=n*(n-1)/2, 0.01<=pi<=0.99

# Analysis

We can build a probability matrix of moving from vertex i to j. Let's call the probability of moving from vertex x to vertex y p(x,y).

Note that we can calculate the probability for each vertex. Suppose that the current vertex is i and f(x,y) denotes the probability to reach state (i,i) from state (x,y).

Certainly, f(i,i) = 1, f(s,s) = 0 for s!=i, and f(x,y) = sigma i = 1 to n sigma j = 1 to n p(x,i) * p(y,j) * f(i,j) for x!=y.

To solve this system, we need to use Gaussian elimination. If we use Gaussian elimination for all vertices, the time complexity will be O(n^7), which is not sufficiant.

After observing the coefficient matrix, we can see that all coefficient matrices in eliminations are the same. Therefore, we can calculate the inverse of the matrix, and multiply it with the value matrix. The row denoting the state of (a,b) will be the answer. With this method, the time complexity is reduced to O(n^6), and we can pass the problem.

# Code


``` C++
#include <stdio.h>
#include <cmath>
#include <algorithm>
using namespace std;
int mp[22][22],deg[22];
double stay[22],go[22][22],lm[484][968],mul[484][22],res[484][22];
const double EPS=1e-10;
int main()
{
	int n,m,a,b;
	scanf("%d%d%d%d",&n,&m,&a,&b);
	--a;
	--b;
	for (int i=0;i<m;++i)
	{
		int u,v;
		scanf("%d%d",&u,&v);
		--u;
		--v;
		mp[u][v]=mp[v][u]=1;
		++deg[u];
		++deg[v];
	}
	for (int i=0;i<n;++i)
		scanf("%lf",stay+i);
	for (int i=0;i<n;++i)
		for (int j=0;j<n;++j)
			go[i][j]=(i==j?stay[i]:mp[i][j]*(1.0-stay[i])/deg[i]);
	for (int i=0;i<n;++i)
		for (int j=0;j<n;++j)
		{
			if (i==j)
			{
				lm[i*n+j][i*n+j]=1.0;
				continue;
			}
			lm[i*n+j][i*n+j]=-1;
			for (int k=0;k<n;++k)
				for (int l=0;l<n;++l)
					lm[i*n+j][k*n+l]+=go[i][k]*go[j][l];
		}
	for (int i=0;i<n;++i)
		for (int j=0;j<n;++j)
			lm[i*n+j][n*n+i*n+j]=1.0;
	int n2=n*n;
	for (int i=0;i<n2;++i)
	{
		int p=i;
		for (int j=i+1;j<n2;++j)
			if (abs(lm[j][i])>abs(lm[p][i]))
				p=j;
		for (int j=0;j<2*n2;++j)
			swap(lm[p][j],lm[i][j]);
		for (int j=2*n2-1;j>=i;--j)
			lm[i][j]/=lm[i][i];
		for (int j=i+1;j<n2;++j)
			if (abs(lm[j][i])>EPS)
			{
				double scale_factor=lm[j][i];
				for (int k=i;k<2*n2;++k)
					lm[j][k]-=scale_factor*lm[i][k];
			}
	}
	for (int i=n2-1;i>=0;--i)
		for (int j=i-1;j>=0;--j)
		{
			double scale_factor=lm[j][i];
			if (abs(scale_factor)>EPS)
				for (int k=0;k<2*n2;++k)
					lm[j][k]-=scale_factor*lm[i][k];
		}
	for (int i=0;i<n;++i)
		mul[i*n+i][i]=1.0;
	for (int i=0;i<n2;++i)
		for (int j=0;j<n;++j)
			for (int k=0;k<n2;++k)
				res[i][j]+=lm[i][n2+k]*mul[k][j];
	for (int i=0;i<n;++i)
		printf("%.10f ",res[a*n+b][i]);
	printf("\n");
	return 0;
}
```
