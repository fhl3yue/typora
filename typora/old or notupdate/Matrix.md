# 【模板】矩阵快速幂

## 题目背景

一个 $m \times n$ 的**矩阵**是一个由 $m$ 行 $n$ 列元素排列成的矩形阵列。即形如

$$ A = \begin{bmatrix} a_{1 1} & a_{1 2} & \cdots & a_{1 n} \\ a_{2 1} & a_{2 2} & \cdots & a_{2 n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m 1} & a_{m 2} & \cdots & a_{m n} \end{bmatrix} \text{.} $$

本题中认为矩阵中的元素 $a_{i j}$ 是整数。

两个大小分别为 $m \times n$ 和 $n \times p$ 的矩阵 $A, B$ **相乘**的结果为一个大小为 $m \times p$ 的矩阵。将结果矩阵记作 $C$，则

$$ c_{i j} = \sum_{k = 1}^{n} a_{i k} b_{k j} \text{,\qquad($1 \le i \le m$, $1 \le j \le p$).} $$

而如果 $A$ 的列数与 $B$ 的行数不相等，则无法进行乘法。

可以验证，矩阵乘法满足结合律，即 $(A B) C = A (B C)$。

一个大小为 $n \times n$ 的矩阵 $A$ 可以与自身进行乘法，得到的仍是大小为 $n \times n$ 的矩阵，记作 $A^2 = A \times A$。进一步地，还可以递归地定义任意高次方 $A^k = A \times A^{k - 1}$，或称 $A^k = \underbrace{A \times A \times \cdots \times A}_{k \text{ 次}}$。

特殊地，定义 $A^0$ 为单位矩阵 $I = \begin{bmatrix} 1 & 0 & \cdots & 0 \\ 0 & 1 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & 1 \end{bmatrix}$。

## 题目描述

给定 $n\times n$ 的矩阵 $A$，求 $A^k$。

## 输入格式

第一行两个整数 $n,k$。  
接下来 $n$ 行，每行 $n$ 个整数，第 $i$ 行的第 $j$ 的数表示 $A_{i,j}$。

## 输出格式

输出 $A^k$

共 $n$ 行，每行 $n$ 个数，第 $i$ 行第 $j$ 个数表示 $(A^k)_{i,j}$，每个元素对 $10^9+7$ 取模。

## 样例 #1

### 样例输入 #1

```
2 1
1 1
1 1
```

### 样例输出 #1

```
1 1
1 1
```

## 提示

**【数据范围】**

对于 $100\%$ 的数据，$1\le n \le 100$，$0 \le k \le 10^{12}$，$|A_{i,j}| \le 1000$。

```c++
const int N = 33;
const ll mod = 1e9 + 7;
struct node {
	ll n,m;
	ll a[N][N] = {};
	void init(ll nn,ll mm) {
		n = nn, m = mm;
		for(int i = 1; i <= nn; i++) 
			a[i][i] = 1ll;
	}
};

node operator * (const node &x,const node &y) {
	node p;
	p.n = x.n, p.m = y.m;
	for(int k = 1;k <= x.m; k ++)
	for(int i = 1;i <= x.n; i ++)
	for(int j = 1;j <= y.m; j ++){
		p.a[i][j] = (p.a[i][j] + x.a[i][k] % mod * y.a[k][j] % mod) % mod;
        p.a[i][j] = (p.a[i][j] + mod) % mod;
	}
	return p;
}

node ksm(node x,ll n) {
	node ans = x;
	while(n) {
		if(n & 1) ans = ans * x;
		x = x * x;
		n >>= 1;
	}
	return ans;
}
```

[转置系数的确定](https://blog.csdn.net/u012061345/article/details/52224623)

