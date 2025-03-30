



**B**

签到 但是wa  dzk见死不救捏

```c++
#include <bits/stdc++.h>
typedef long long ll;

void solve() {
	int n;
	std::cin >> n;
	std::vector<ll> a(n);
	for(int i = 0; i < n; i++) {
		std::cin >> a[i];
	}
	ll L,R,res = 0,cur = 0, pre = 0,cnt = 0;
	std::cin >> L >> R;
	for(int i = 0; i < n; i++) {
		if(a[i] < L) res += (L - a[i]);
		if(a[i] > R) cnt += (a[i] - R);
		if(L <= a[i] && a[i] <= R) {
			cur += (a[i] - L);
			pre += (R - a[i]);
		}
	}
	ll ans = std::max(res,cnt);
	if(ans == res) {
		if(cur >= ans - cnt)
			std::cout << ans << '\n';
		else {
			std::cout << -1 << '\n';
		}
	}
	else {
		if(pre >= ans - res) 
			std::cout << ans << '\n';
		else {
			std::cout << -1 << '\n';
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

```c++
#include <bits/stdc++.h>
typedef long long ll;

void solve() {
	int n;
	std::cin >> n;
	std::vector<ll> a(n);
	for(int i = 0; i < n; i++) {
		std::cin >> a[i];
	}
	ll L,R,res = 0,sum = 0,cnt = 0;
	std::cin >> L >> R;
	for(int i = 0; i < n; i++) {
		if(a[i] < L) res += (L - a[i]);
		if(a[i] > R) cnt += (a[i] - R);
		sum += a[i];
	}
	ll ans = std::max(res,cnt);
	if(sum > n * R || sum < n * L) {
		std::cout << -1 << '\n';
		return;
	}
	std::cout << ans << '\n';
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



**D**

区间修改 单点查询 板子题  用的树状数组

```c++
#include <bits/stdc++.h>
typedef long long ll;

void solve() {
	int n,now = 0;
	std::cin >> n;
	std::vector<ll> a(n+1),c(n+1);
	auto lowbit = [&] (ll x) -> ll {
		return x & (-x);	
	};
	auto update = [&] (ll x, ll k) -> void {
		for(ll i = x; i <= n; i += lowbit(i)) 
			c[i] += k;
	};
	auto query = [&] (ll x) -> ll {
		ll sum = 0;
		for(ll i = x; i > 0; i -= lowbit(i)) 
			sum += c[i];
		return sum;
	};

	for(int i = 1; i <= n; i++) {
		std::cin >> a[i];
		update(i,a[i] - now);
		now = a[i];
	}
	int m;
	std::cin >> m;
	for(ll i = 1,p,l,r,d,x; i <= m; i++) {
		std::cin >> p;
		if(p == 1) {
			std::cin >> l >> r >> d;
			update(l,d);
			update(r+1,-d);
		}
		else {
			std::cin >> x;
			std::cout << query(x) << '\n';
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

**E**

线性筛 + 枚举

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 1e5 + 50;
bool not_prime[N];
ll plist[N], cnt;
void init()
{
    for(int i = 2;i < N; i++)
    {
        if(not_prime[i] == 0) plist[++cnt] = i;
        for(int j=1;j<=cnt;j++)
        {
            int x;
            x = i * plist[j];
            if(x > N) break;
            not_prime[x] = 1;
            if(i % plist[j] == 0) break;
        }
    }
}
void solve()
{
    int n;
    std::cin >> n;
    bool ok = false;
    std::vector<int> v;
    //std::cout <<  cnt << '\n';
    for(int i = 1; i <= cnt; i++) {
        int t = plist[i];
        for(int j = 1; j <= cnt; j ++) {
            if(plist[j] < n - t && not_prime[n - t - plist[j]] == 0) {
                std::cout << t << " " << plist[j] <<" "<< n - t - plist[j]<< "\n";
                ok = true;
                return;
            }

        }
    }
    if(!ok) std::cout << -1 << "\n";
    return;
}
int main()
{
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    init();
    int _ = 1;
    std::cin >> _ ;
    while(_ --) {
        solve();
    }
    return 0;
}

```

**G**

爬楼梯  递推+打表+取模

```c++
#include <bits/stdc++.h>
typedef long long ll;
const ll mod = 1e9 + 7;
const int N = 1e6 + 50;
ll f[N];
void solve() {
	int n;
	std::cin >> n;
	f[1] = 1, f[2] = 2, f[3] = 4;
	for(int i = 4; i <= n; i++) {
		f[i] = (((f[i-1] + f[i-2]) % mod + f[i-3]) %mod + mod) % mod; 
	}
	std::cout << f[n] << '\n';
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

**H**

查询区间最大值 

$RMQ$板子

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 1e6 + 50;
typedef long long ll;
const int M = 2007;
int f[N][30];

void solve() {
	int n;
	std::cin >> n;
	std::vector<int> a(n+1),Log(n+1);
	for(int i = 1; i <= n; i++) std::cin >> a[i];

	for(int i = 1; i <= n; i++) f[i][0] = a[i];
	Log[1] = 0, Log[2] = 1;
	for(int i = 3; i <= n; i++) Log[i] = Log[i/2] + 1;
	for(int j = 1; j <= Log[n]; j ++) {
		for(int i = 1; i + (1 << j) - 1 <= n; i++) {
			f[i][j] = std::max(f[i][j-1],f[i + (1 <<(j-1))][j-1]);
		}
	}
	int q;
	std::cin >> q;
	for(int i = 1; i <= q; i++) {
		int l,r;
		std::cin >> l >> r;
		int p = Log[r - l + 1];
		int ans = std::max(f[l][p],f[r - (1 << p) + 1][p]);
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

**i**

三分  求极值

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;

void solve()
{
    int n;
    std::cin >> n;
    std::vector<ll> a(n + 1), c(n + 1);
    for(int i = 1; i <= n; i++) std::cin >> c[i];

    auto check = [&](ll x) -> ll {
        ll res = 0;
        for(int i = 1; i <= n; i++) {
            res += std::abs(c[i] - 1ll * x);
        }
        return res;
    };

    ll l = 0, r = 1e10;
    ll ans = 1e14 + 7;
    while(r - l > 1) {
			ll mid = l + r >> 1;
			ll lmid = mid - 1;
			ll rmid = mid + 1;
			if(check(lmid) < check(rmid)) r = mid;
			else l = mid;
	}
    //std::cout << l << ' ' << r << '\n';
	ans = std::min({ans,check(l),check(r)});
    std::cout << ans + 1 << '\n';
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

**j**

开方签到题

```c++
#include <bits/stdc++.h>
typedef long long ll;

void solve() {
	ll n;
	std::cin >> n;
	std::cout << int(std::sqrt(n)) << '\n';
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



**K**

s - t 的一条路径   要求路径的最大值最小

二分 + dijkstra判断联通

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
const int INF = 0x3f3f3f3f;
struct  edge{
    int from;
    int to;
    int dis;
    int next;
}e[N];
int head[N],cnt;
void add(int u,int v,int w)
{
     ++cnt;
     e[cnt].from = u;
     e[cnt].to = v;
     e[cnt].dis = w;
     e[cnt].next = head[u];
     head[u] = cnt;
}

struct node{
    int dis;
    int pos;
    bool operator <(const node &x)const
    {
        return x.dis < dis;
    }
};

void solve()
{
    int n,m;
    std::cin >> n >> m;
    std::vector<int> a(m),b(m),c(m);
    for(int i = 0; i < m; ++ i) {
        std::cin >> a[i] >> b[i] >> c[i];
    }
    int s,t;
    std::cin >> s >> t;
    auto check = [&](int x) -> bool {
        for(int i = 0; i < N; i++) {
            head[i] = 0;
            e[i] = {0,0,0,0};
        }   cnt = 0;
        for(int i = 0; i < m; ++ i) {
            if(c[i] <= x) {
                add(a[i], b[i], c[i]);
                add(b[i], a[i], c[i]);
            }
        }
        std::vector<int> f(n+1);
        std::vector<bool> vis(n+1,false);
        for(int i = 1; i <= n; ++ i) f[i] = INF;
        f[s] = 0;
        std::priority_queue<node> q;
        q.push((node){0,s});
        while(!q.empty()) {
            node p = q.top();
            q.pop();
            int x = p.pos;
            if(vis[x]) continue;
            vis[x] = true;
            for(int i = head[x]; i; i = e[i].next) {
                int y = e[i].to;
                if(f[y] > f[x] + e[i].dis) {
                    f[y] = f[x] + e[i].dis;
                    q.push((node){f[y],y});
                }
            }
        }
        return f[t] != INF;
    };
    int l = 0, r = 1e4, x = 0;
    while(l <= r) {
        int mid = (l + r) >> 1;
        if(check(mid)) {
            x = mid;
            r = mid - 1;
        }
        else{
            l = mid + 1;
        }
    }
    std::cout << x << '\n';
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

**F**

题目题意是 1 到各点最短距离 + 各点到1最短距离

但是  $1\le n,m\le 10^6$ 单向边    n次dijkstra  = $n*n*log n$

之前的 $johnson$ 全源最短路 $O(nmlogm)$ 也不行

$Floyed$ 更是不行 

so cant  dzk ngmay 

在dzk 的亲切指导下，我动力只要建反向边 再跑一遍就是各点到 1 的距离

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
const int INF = 0x3f3f3f3f;
struct node{
    int dis;
    int pos;
    bool operator <(const node &x) const {
        return x.dis < dis;
    }
};
struct edge{
    int to;
    int dis;
    int next;
}e[N];
int head[N],cnt;
void add(int u,int v,int w){
    e[++cnt] = (edge){v,w,head[u]};
    head[u] = cnt;
}
void solve()
{
    int n,m;
    std::cin >> n >> m;
    std::vector<int> a(m),b(m),c(m);
    for(int i = 0;i < m;++i) {
        std::cin >> a[i] >> b[i] >> c[i];
    }
    ll ans = 0;
    auto Dijkstra = [&](int s) -> void{
        std::vector<int> f(n+1);
        std::vector<bool> vis(n+1,false);
        for(int i = 1; i <= n; ++ i) f[i] = INF;
        f[s] = 0;
        std::priority_queue<node> q;
        q.push((node){0,s});
        while(!q.empty()) {
            node p = q.top();
            q.pop();
            int x = p.pos;
            if(vis[x]) continue;
            vis[x] = true;
            for(int i = head[x]; i; i = e[i].next) {
                int y = e[i].to;
                if(f[y] > f[x] + e[i].dis) {
                    f[y] = f[x] + e[i].dis;
                    q.push((node){f[y],y});
                }
            }
        }
        for(int i = 2; i <= n; i++) ans += 1ll * f[i];
    };


    for(int i = 0;i < m;++i) {
        add(a[i],b[i],c[i]);
    }
    Dijkstra(1);
    
    for(int i = 0; i <= cnt; i ++) {
        e[i] = {0,0,0};
    }   std::memset(head,0,sizeof(head)); cnt = 0;
    
    for(int i = 0;i < m;++i) {
        add(b[i],a[i],c[i]);
    }
    Dijkstra(1);

    std::cout << ans << '\n';
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

