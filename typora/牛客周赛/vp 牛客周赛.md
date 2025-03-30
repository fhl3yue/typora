**vp 牛客周赛**

**52**

小红有 $n$ 个数字 $a_1, a_2, \dots, a_n$ 和一个空字符串 $s$。现在她需要执行 $n$ 次操作：第 $i$ 次操作需要将 $a_i$ 按照数位上的相对顺序、从左到右的取出并依次插入 $s$（在 $s$ 中不需要连续，但需要保持原有相对顺序）。 小红想要构造一个这样的字符串 $s$，使得它的字典序是所有合法构造方案中最大的。

```c++
2
92 86
9862
```

小学哥完美的优先队列   直接给搞成模拟了

```c++
#include <bits/stdc++.h>
typedef long long ll;
std::priority_queue< std::pair<char,std::string> > q;
void solve() {
	int n;
	std::cin >> n;
	for(int i = 1; i <= n; i++) {
		std::string s;
		std::cin >> s;
		q.push({s[0],s});
	}
	std::string ans;
	while(!q.empty()) {
		auto [c,s] = q.top(); 
		q.pop();
		ans += c;
		s.erase(0,1);
		if(s != "") {
			q.push({s[0],s});
		}
	}
	std::cout << ans <<'\n';
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



**51**

给定一个 `n×n` 的矩阵，矩阵中的每个元素都是正整数，小红当前位于左上角 `(1, 1)`，每次可以从 `(x, y)` 走到 `(x+1, y)`、`(x, y+1)`、`(x-1, y)`、`(x, y-1)`，但不能走出矩阵。小红希望找到一条到右下角 `(n, n)` 的路径，定义路径权值为路径上经过的每个点的最大值，求所有路径中的最小路径权值。

以为是dp 问题  却没发现是   二分最大点值  判断能否从起点到终点即可

```c++
#include <bits/stdc++.h>
typedef long long ll;
int a[1000][1000];
std::vector< std::pair<int,int> > d = {{0,1},{0,-1},{1,0},{-1,0}};
bool vis[600][600];
int n;

void dfs(int x,int y,int w) {
	if(a[x][y] > w || vis[x][y] || vis[n][n]) return;
	vis[x][y] = 1;
	for(auto [i,j] : d) {
		i += x; j += y;
		if(vis[i][j] || i < 1 || i > n || j < 1 || j > n || a[x][y] > w) continue;
		dfs(i,j,w);
	}
}

void solve() {
    std::cin >> n;
    for(int i = 1; i <= n; i++) {
        for(int j = 1; j <= n; j++) {
            std::cin >> a[i][j];
        }
    }
    if(n == 1) {
    	std::cout << a[1][1] << '\n';
    	return;
    }
    int l = 1, r = 1e9, x = 0;
    while(l <= r) {
    	int mid = (l + r) >> 1;
    	std::memset(vis,0,sizeof(vis));
    	dfs(1,1,mid);
    	if(vis[n][n]) {
    		r = mid - 1;
    		x = mid;
    	}
    	else l = mid + 1;
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

学习到了 遍历四个方向

```c++
std::vector< std::pair<int,int> > d = {{0,1},{0,-1},{1,0},{-1,0}};
for(auto [i,j] : d) {
		i += x; j += y;
		if(vis[i][j] || i < 1 || i > n || j < 1 || j > n || a[x][y] > w) continue;
		dfs(i,j,w);
}
```



**50 **

小红有一棵 `n` 个点的树，根节点为 `1`，有一个物块在根节点上，每次它会等概率随机移动到当前节点的其中一个子节点，而后等概率随机传送到一个同深度节点，若此时它位于叶子节点，则停止移动。 求其移动到子节点的次数的期望值，答案对 `998244353` 取模。

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
const int mod = 998244353;

ll ksm(ll a,ll b) {
	ll ans = 1;
	while(b) {
		if(b & 1) ans = ans * a % mod;
		a = a * a % mod;
		b >>= 1;
	}
	return ans;
}
std::vector<int> e[N];
int a[N],b[N],dep[N];
ll p[N];
ll ans = 0;
int maxdep = -1;
void dfs(int u,int fa) {
	dep[u] = dep[fa] + 1;
	a[dep[u]] += 1;
	maxdep = std::max(maxdep,dep[u]);
	b[dep[u]] += (u != 1 && e[u].size() == 1);// 仅存在一条回边 说明子叶节点

	for(int i = 0; i < e[u].size(); i++) {
		int v = e[u][i];
		if(v == fa) continue;
		dfs(v,u);
	}
}
void solve() {
	int n;
	std::cin >> n;
	if(n == 1) {
		std::cout << 0 << '\n';
		return;
	}
	for(int i = 1,u,v; i <= n - 1; i++) {
		std::cin >> u >> v;
		e[u].push_back(v);
		e[v].push_back(u);
	}
	dfs(1,0);
	p[1] = 1;
	for(int i = 2; i <= maxdep; i++) {
		p[i] = p[i-1] * (a[i] - b[i]) % mod * ksm(a[i],mod - 2) % mod;
	}
	for(int i = 1; i <= maxdep; i ++) {
		ans += p[i];
		ans %= mod;
	}
	std::cout << ans <<'\n';
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

一般除法取模转化为乘法逆元就用费马小定理就好  $ksm(a,p-2)$  

**49**

$1\le T \le 2 \times 10 ^ 5$   $1 \le l \le r \le 10^{18}$  

$[l,r]$ 区间所有整数的异或和  

异或有结合律，且$4k,4k+1,4k+2,4k+3$  异或和为0

```c++
#include <bits/stdc++.h>
typedef long long ll;

ll ntum(ll x) {
	// 0 1 2 3 ^ -> 0 
	ll res = 0; // 5 ->(0 ^ 5 ^ 4)
	ll k = (x + 1) % 4; // 次数 
	while(k--) {
		res ^= x;
		x --;
	}
	return res;
}
void solve() {
	ll l,r;
	std::cin >> l >> r;
	std::cout << (ntum(r)^ntum(l-1)) << '\n';
	return;
}

int main() {
	std::ios::sync_with_stdio(false);
	std::cin.tie(nullptr);
	int _ = 1;
	std::cin >> _;
	while(_ --) {
		solve();
	}
	return 0;
}
```

希望找到一个最小的正整数$k$,  使得对于数组$a$中的某些索引$i$, 满足 $a_{i} + a_{i+2k} = 2 \times a_{i+k}$

$hash(1,n-2\times k) + hash(2\times k + 1,n) = 2\times hash(k+1,n-2\times k)$

```c++
#include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
const int p = 13331;
const int mod = 1e9 + 7;
const int N = 2e6 + 50;
ull P[N];
ull h[N];
ull _hash(int l,int r) {
	if(l < 0 || r < 0) return 0;
	return (h[r] - h[l - 1] * P[r - l + 1] % mod + mod) % mod;
}
void solve() {
	int n;
	std::cin >> n;
	std::vector<ull> a(n+1);
	for(int i = 1; i <= n; i++) {
		std::cin >> a[i];
	}
	P[0] = 1;
	for(int i = 1; i <= n; i++) {
		P[i] = P[i-1] * p;  P[i] %= mod;
		h[i] = h[i-1] * p + a[i]; h[i] %= mod;
	}
	for(int k = 1; k <= n; k++) {
		if( (_hash(1,n-2*k) + _hash(2*k+1,n)) % mod == (2 * _hash(k+1,n-k)) % mod ) {
			std::cout << k <<'\n';
			break;
		}
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



 **46**

Taki买了 `n` 种猫粮，第 `i` 种猫粮的营养值为 `a[i]`、数量为 `b[i]`。猫猫的饭量是无穷的，每一天她可以吃任意数量的猫粮，但同一种猫粮她一天只会吃一次。Taki想知道在 `k` 天内，猫猫可以获得的最大营养值之和是多少。

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
const int  p = 1e9 + 7;

struct node{
    int a,b;
};
void solve()
{
    int n;
    std::cin >> n;
    std::vector<node> t(n+1);
    for(int i = 1;  i <= n; i++) {
        std::cin >> t[i].a;
    }
    for(int i = 1;  i <= n; i++) {
        std::cin >> t[i].b;
    }
    std::sort(t.begin()+1,t.end(),[](node A,node B){
        return A.b < B.b;
    });
    int q,k;
    std::vector<ll> sum(n+1),pre(n+2);
    for(int i = 1; i <= n; i++) {
        sum[i] = sum[i-1] + 1ll * t[i].a * t[i].b;
    }
    for(int i = n; i >= 1; i--) {
        pre[i] = pre[i+1] + t[i].a;
    }
    std::cin >> q;
    while(q --) {
        std::cin >> k;
        int l = 1,r = n,x = 0;
        while(l <= r) {
            int mid = (l + r) >> 1;
            if(t[mid].b <= k) {
                l = mid + 1;
                x = mid;
            }
            else r = mid - 1;
        }
        std::cout << sum[x] + 1ll * pre[x+1] * k << '\n';
    }
    
    return;
}
int main()
{
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    int _ = 1;
    //std::cin >> _ ;
    while(_ --) {
        solve();
    }
    return 0;
}

```

多组数据$t$, 有两个数字 `x`, `y`，她想知道，有多少种方式可以将 `x` 拆成 `y` 个正整数的乘积。 例如 `x=6`, `y=2` 时，有 `6×1=6`, `3×2=6`, `2×3=6`, `1×6=6` 这 4 种方法。 由于这个答案可能很大，因此你需要输出答案对 `10^9 + 7` 取模后的结果。

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
const int p = 1e9 + 7;

ll fac[1001];
ll ksm(ll a,ll b) {
    ll res = 1;
    while(b) {
        if(b & 1) res = res * a % p;
        a = a * a % p;
        b >>= 1;
    }
    return res;
}
void init() {
    fac[0] = 1;
    for(int i = 1; i < 1000; i ++) {
        fac[i] = fac[i - 1] * i % p;
    }
    return;
}
void solve()
{
    int A,B;
    std::cin >> A >> B;
    // A 拆成 B 个 数 乘积 方案数 [12,1] 与 [1,12] 不同  
    std::vector<int> d;
    for(int i = 2; i * i <= A; i ++) {
        if(A % i == 0) {
            int cnt = 0;
            while(1) {
                A /= i;
                cnt ++;
                if(A % i != 0) break;
            }
            d.push_back(cnt);
        }
    }
    if(A > 1) d.push_back(1);
    ll ans = 1;
    for(auto n : d) {
        ll temp = 1;
        for(ll i = B; i <= B - 1 + n; i++) temp = temp * i % p; 
        ans = ans * temp % p * ksm(fac[n],p-2);
        ans %= p;
    }
    std::cout << ans << "\n";
    return;
}
int main()
{
    init();
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    int _ = 1;
    std::cin >> _ ;
    while(_ --) {
        solve();
    }
    return 0;
}

```



