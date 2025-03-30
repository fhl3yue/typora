 

差分约束系统

  

**一、何为差分约束系统：**

差分约束系统（system of difference constraints），是求解关于一组变数的特殊[不等式](https://so.csdn.net/so/search?q=%E4%B8%8D%E7%AD%89%E5%BC%8F&spm=1001.2101.3001.7020)组之方法。如果一个系统由n个变量和m个约束条件组成，其中每个约束条件形如$x_j$-$x_i$<= A(i,j∈\[1,n\]),则称其为差分约束系统(system of difference constraints)。亦即，差分约束系统是求解关于一组变量的特殊不等式组的方法。

通俗一点地说，差分约束系统就是一些不等式的组，而我们的目标是通过给定的约束不等式组求出最大值或者最小值或者差分约束系统是否有解。

比如：

![](https://img-blog.csdn.net/20161222214143171?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY29uc2Npb3VzbWFu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  

**二、差分约束系统的求解：**

差分约束系统可以转化为图论来解决，对应于上面的不等式组，如果要求出$x_3-x_0$的最大值的话，叠加不等式可以推导出$x3-x0$<=7,最大值即为7，我们可以通过建立一个图，包含6个顶点，对每个$x_j - x_i$ <= A，建立一条i到j的有向边，权值为A。通过求出这个图的$x_0$到$x_3$的最短路可以知道也为7，这是巧合吗？并不是。

之所以差分约束系统可以通过图论的最短路来解，是因为$x_j - x_i = A$，会发现它类似最短路中的三角不等式d\[v\] <=d\[u\]+w\[u,v\]，即d\[v\]-d\[u\]<=w\[u,v\]。而求取最大值的过程类似于最短路算法中的松弛过程。

三角不等式：（在此引用大牛的博客）

B - A <= c     (1)

C - B <= a     (2)

C - A <= b     (3)

 如果要求C-A的最大值，可以知道max（C-A）= min(b,a+c),而这正对应了下图中C到A的最短路。 

                                ![](https://img-blog.csdn.net/20161222125003116?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY29uc2Npb3VzbWFu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)  

**因此，对三角不等式加以推广，变量n个，不等式m个，要求xn-x1的最大值，便就是求取建图后的最短路。**

**同样地，如果要求取差分约束系统中xn-x1的最小值，便是求取建图后的最长路。最长路可以通过spfa求出来，只需要改下松弛的方向即可，即if(d\[v\] < d\[u\] + dist(u,v)) d\[v\] = d\[u\] + dist(u,v)。当然我们可以把图中所有的边权取负，求取最短路，两者是等价的。**

**最长路求解算法证明如下：**

[http://www.cnblogs.com/g0feng/archive/2012/09/13/2683880.html](http://www.cnblogs.com/g0feng/archive/2012/09/13/2683880.html)

**最后一点，建图后不一定存在最短路/最长路，因为可能存在无限减小/增大的负环/正环，题目一般会对应于不同的输出。判断差分约束系统是否存在解一般判环即可。**

**3、差分约束系统的应用**

差分约束系统的应用很广，都会有一定的背景，我们只需要根据题意构造出差分约束系统，然后再根据题目的要求求解就行了。

一般题目会有三种情况：(1)、求取最短路 (2)、求取最长路 (3)、判断差分约束系统的解是否存在

当然这三种也可能会相互结合。

**差分约束系统的解法如下：**

**1、  根据条件把题意通过变量组表达出来得到不等式组，注意要发掘出隐含的不等式，比如说前后两个变量之间隐含的不等式关系。**

**2、  进行建图：**

**首先根据题目的要求进行不等式组的标准化。**

**(1)、如果要求取最小值，那么求出最长路，那么将不等式全部化成$x_i – x_j >= k$的形式，这样建立j->i的边，权值为k的边，如果不等式组中有$x_i – x_j > k$，因为一般题目都是对整形变量的约束，化为$x_i – x_j >= k + 1$即可，如果$x_i – x_j = k$呢，那么可以变为如下两个：$x_i – x_j >= k$,$x_i – x_j <= k$,进一步变为$x_j – x_i >= -k$，建立两条边即可。**

**(2)、如果求取的是最大值，那么求取最短路，将不等式全部化成$x_i – x_j <= k$的形式, 这样建立j->i的边，权值为k的边，如果像上面的两种情况，那么同样地标准化就行了。**

**(3)、如果要判断差分约束系统是否存在解，一般都是判断环，选择求最短路或者最长路求解都行，只是不等式标准化时候不同，判环地话，用spfa即可，n个点中如果同一个点入队超过n次，那么即存在环。**

**值得注意的一点是：建立的图可能不联通，我们只需要加入一个超级源点，比如说求取最长路时图不联通的话，我们只需要加入一个点S，对其他的每个点建立一条权值为0的边图就联通了，然后从S点开始进行spfa判环。最短路类似。**

**3、  建好图之后直接spfa或bellman-ford求解，不能用dijstra算法，因为一般存在负边，注意初始化的问题。**

  

[[SCOI2011\]糖果](https://ac.nowcoder.com/acm/problem/20284)

```c++
#include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
const int N = 2e5 + 4;
const ll mod = 1e9 + 7;
std::vector< std::pair<int,int> > edge[N];
int num[N],dis[N];
bool vis[N];
bool spfa(int u,int n) {
	std::queue<int> q; q.push(u);
	std::memset(dis,-0x3f,sizeof(dis)); dis[u] = 0;
	vis[u] = true;
	int count = 0;
	while(!q.empty()){
		int t = q.front();
		q.pop();
		vis[t] = false;
		for(int i = 0; i < edge[t].size(); i++) {
			auto [x,y] = edge[t][i];
			if(dis[x] < dis[t] + y) { // disv < disu + w
				dis[x] = dis[t] + y;
				num[x] = num[t] + 1;
				if(num[x] >= n + 1) return false;
				if(++count >= 4 * n) return false;
				if(!vis[x]) {
					q.push(x);
					vis[x] = true;
				}
			}
		}
	}
	return true;
}
void solve() {
	int n,k;
	std::cin >> n >> k;
	for(int i = 1; i <= n; i++) edge[0].push_back({i,1});//每个小朋友都能够至少分到1k糖果 
	while(k --) {
		int x,a,b;
		std::cin >> x >> a >> b;
		if(x == 1) {
			edge[b].push_back({a,0});
			edge[a].push_back({b,0});
		}
		if(x == 2) edge[a].push_back({b,1});
		if(x == 3) edge[b].push_back({a,0});
		if(x == 4) edge[b].push_back({a,1});
		if(x == 5) edge[a].push_back({b,0});
	}
	if(!spfa(0,n)) std::cout << -1 << '\n';
	else {
		ll ans = 0;
		for(int i = 1; i <= n; i++) ans += dis[i];
		std::cout << ans << '\n';
	}
	return;
}

int main() {
	std::ios::sync_with_stdio(false);
	std::cin.tie(nullptr);
	int _ = 1;
	//std::cin >> _;
	while(_ --) {
		solve();
	}
	return 0;
}
```

