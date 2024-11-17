

小红有一棵树，初始所有点都是白色。小红最多可以染黑 $k$个点，定义染色后树的权值为白色点对距离的最大值，求最小的权值。$n$个点，$n-1$ 条边。 

染黑$k$个点，转换为染白$n-k = m$个点。

二分树的权值，范围$[0,m]$ 

$dep[i][j]$  表示 $i$子树 选择 $j$个节点的最小深度。



<img src="https://cdn.luogu.com.cn/upload/image_hosting/zsv97ky8.png" style="zoom:33%;" />



```c++
void dfs(int x,int fa) {  树上dp
	siz[x] = 1;
	dep[x][0] = 0;
	dep[x][1] = 1;
	for(int i = 2; i <= m; i++) {
		dep[x][i] = n + 1; // 不可能的大值
	}
	for(int y : e[x]) {
		if(y == fa) continue;
		dfs(y,x);
		for(int j = std::min(m,siz[x]); j >= 0; j--) {
			for(int k = std::min(m - j, siz[y]); k >= 0; k --) { // 枚举各子树选几个 
				if(j != 0 && k != 0 && dep[x][j] + dep[y][k] - 1 > mid) continue;
				dep[x][j+k] = std::min(dep[x][j+k],std::max(dep[x][j],dep[y][k] + 1));
			}
		}
		siz[x] += siz[y];
	}
	return;
}
```



```c++
#include <bits/stdc++.h>
typedef long long ll;
int n,k,m,mid;
const int N = 3e3 + 50;
int dep[N][N];// i子树 选 j个节点 深度最小
int siz[N];
std::vector<int> e[N << 1];

void dfs(int x,int fa) {
	siz[x] = 1;
	dep[x][0] = 0;
	dep[x][1] = 1;
	for(int i = 2; i <= m; i++) {
		dep[x][i] = n + 1;
	}
	for(int y : e[x]) {
		if(y == fa) continue;
		dfs(y,x);
		for(int j = std::min(m,siz[x]); j >= 0; j--) {
			for(int k = std::min(m - j, siz[y]); k >= 0; k --) {
				if(j != 0 && k != 0 && dep[x][j] + dep[y][k] - 1 > mid) continue;
				dep[x][j+k] = std::min(dep[x][j+k],std::max(dep[x][j],dep[y][k] + 1));
			}
		}
		siz[x] += siz[y];
	}
	return;
}
void solve() {
	std::cin >> n >> k;
	m = n - k;
	for(int i = 1,x,y; i < n; i++) {
		std::cin >> x >> y;
		e[x].push_back(y);
		e[y].push_back(x);
	}
	int l = 0, r = m,x;
	while(l <= r) {
		mid = (l + r) >> 1;
		dfs(1,0);
		if(dep[1][m] == n + 1) l = mid + 1;
		else {
			x = mid;
			r = mid - 1;
		}
	}
	std::cout << x << '\n';
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

