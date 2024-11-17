### 佛祖

long long : 9,223,372,036,854,775,807  =  9 * $10^{18}$

```c++
//
//                            _ooOoo_
//                           o8888888o
//                           88" . "88
//                           (| -_- |)
//                           O\  =  /O
//                        ____/`---'\____
//                      .'  \|     |//  `.
//                     /  \|||  :  |||//  \
//                    /  _||||| -:- |||||-  \
//                    |   | \  -  /// |   |
//                    | \_|  ''\---/''  |   |
//                    \  .-\__  `-`  ___/-. /
//                  ___`. .'  /--.--\  `. . __
//               ."" '<  `.___\_<|>_/___.'  >'"".
//              | | :  `- \`.;`\ _ /`;.`/ - ` : | |
//              \  \ `-.   \_ __\ /__ _/   .-` /  /
//         ======`-.____`-.___\_____/___.-`____.-'======
//                            `=---='
//        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
//                     佛祖保佑      永无BUG
```



### __int128

```c++
using i128 = __int128;
i128 read()
{
	i128 flag=1,num=0;
	char cum=getchar();
	while(cum<'0' || cum>'9'){if(cum=='-')flag=-1;cum=getchar();}
	while(cum>='0' && cum<='9'){num=(num<<3)+(num<<1)+(cum-'0');cum=getchar();}
	return flag*num;
}

std::ostream &operator<<(std::ostream &os, i128 n) {
    std::string s;
    while (n) {
        s += '0' + n % 10;
        n /= 10;
    }
    std::reverse(s.begin(), s.end());
    return os << s;
}

```



### 取模 

```c++
template<class T>
constexpr T power(T a, i64 b) {
    T res = 1;
    for (; b; b /= 2, a *= a) {
        if (b % 2) {
            res *= a;
        }
    }
    return res;
}

constexpr i64 mul(i64 a, i64 b, i64 p) {
    i64 res = a * b - i64(1.L * a * b / p) * p;
    res %= p;
    if (res < 0) {
        res += p;
    }
    return res;
}
template<i64 P>
struct MLong {
    i64 x;
    constexpr MLong() : x{} {}
    constexpr MLong(i64 x) : x{norm(x % getMod())} {}
    
    static i64 Mod;
    constexpr static i64 getMod() {
        if (P > 0) {
            return P;
        } else {
            return Mod;
        }
    }
    constexpr static void setMod(i64 Mod_) {
        Mod = Mod_;
    }
    constexpr i64 norm(i64 x) const {
        if (x < 0) {
            x += getMod();
        }
        if (x >= getMod()) {
            x -= getMod();
        }
        return x;
    }
    constexpr i64 val() const {
        return x;
    }
    explicit constexpr operator i64() const {
        return x;
    }
    constexpr MLong operator-() const {
        MLong res;
        res.x = norm(getMod() - x);
        return res;
    }
    constexpr MLong inv() const {
        assert(x != 0);
        return power(*this, getMod() - 2);
    }
    constexpr MLong &operator*=(MLong rhs) & {
        x = mul(x, rhs.x, getMod());
        return *this;
    }
    constexpr MLong &operator+=(MLong rhs) & {
        x = norm(x + rhs.x);
        return *this;
    }
    constexpr MLong &operator-=(MLong rhs) & {
        x = norm(x - rhs.x);
        return *this;
    }
    constexpr MLong &operator/=(MLong rhs) & {
        return *this *= rhs.inv();
    }
    friend constexpr MLong operator*(MLong lhs, MLong rhs) {
        MLong res = lhs;
        res *= rhs;
        return res;
    }
    friend constexpr MLong operator+(MLong lhs, MLong rhs) {
        MLong res = lhs;
        res += rhs;
        return res;
    }
    friend constexpr MLong operator-(MLong lhs, MLong rhs) {
        MLong res = lhs;
        res -= rhs;
        return res;
    }
    friend constexpr MLong operator/(MLong lhs, MLong rhs) {
        MLong res = lhs;
        res /= rhs;
        return res;
    }
    friend constexpr std::istream &operator>>(std::istream &is, MLong &a) {
        i64 v;
        is >> v;
        a = MLong(v);
        return is;
    }
    friend constexpr std::ostream &operator<<(std::ostream &os, const MLong &a) {
        return os << a.val();
    }
    friend constexpr bool operator==(MLong lhs, MLong rhs) {
        return lhs.val() == rhs.val();
    }
    friend constexpr bool operator!=(MLong lhs, MLong rhs) {
        return lhs.val() != rhs.val();
    }
};

template<>
i64 MLong<0LL>::Mod = i64(1E18) + 9;

template<int P>
struct MInt {
    int x;
    constexpr MInt() : x{} {}
    constexpr MInt(i64 x) : x{norm(x % getMod())} {}
    
    static int Mod;
    constexpr static int getMod() {
        if (P > 0) {
            return P;
        } else {
            return Mod;
        }
    }
    constexpr static void setMod(int Mod_) {
        Mod = Mod_;
    }
    constexpr int norm(int x) const {
        if (x < 0) {
            x += getMod();
        }
        if (x >= getMod()) {
            x -= getMod();
        }
        return x;
    }
    constexpr int val() const {
        return x;
    }
    explicit constexpr operator int() const {
        return x;
    }
    constexpr MInt operator-() const {
        MInt res;
        res.x = norm(getMod() - x);
        return res;
    }
    constexpr MInt inv() const {
        assert(x != 0);
        return power(*this, getMod() - 2);
    }
    constexpr MInt &operator*=(MInt rhs) & {
        x = 1LL * x * rhs.x % getMod();
        return *this;
    }
    constexpr MInt &operator+=(MInt rhs) & {
        x = norm(x + rhs.x);
        return *this;
    }
    constexpr MInt &operator-=(MInt rhs) & {
        x = norm(x - rhs.x);
        return *this;
    }
    constexpr MInt &operator/=(MInt rhs) & {
        return *this *= rhs.inv();
    }
    friend constexpr MInt operator*(MInt lhs, MInt rhs) {
        MInt res = lhs;
        res *= rhs;
        return res;
    }
    friend constexpr MInt operator+(MInt lhs, MInt rhs) {
        MInt res = lhs;
        res += rhs;
        return res;
    }
    friend constexpr MInt operator-(MInt lhs, MInt rhs) {
        MInt res = lhs;
        res -= rhs;
        return res;
    }
    friend constexpr MInt operator/(MInt lhs, MInt rhs) {
        MInt res = lhs;
        res /= rhs;
        return res;
    }
    friend constexpr std::istream &operator>>(std::istream &is, MInt &a) {
        i64 v;
        is >> v;
        a = MInt(v);
        return is;
    }
    friend constexpr std::ostream &operator<<(std::ostream &os, const MInt &a) {
        return os << a.val();
    }
    friend constexpr bool operator==(MInt lhs, MInt rhs) {
        return lhs.val() == rhs.val();
    }
    friend constexpr bool operator!=(MInt lhs, MInt rhs) {
        return lhs.val() != rhs.val();
    }
};

template<>
int MInt<0>::Mod = 998244353;

template<int V, int P>
constexpr MInt<P> CInv = MInt<P>(V).inv();

constexpr int P = 1000000007;
using Z = MInt<P>;
```

### 组合数 Comb, with. MInt & MLong

```c++
struct Comb {
    int n;
    std::vector<Z> _fac;
    std::vector<Z> _invfac;
    std::vector<Z> _inv;
    
    Comb() : n{0}, _fac{1}, _invfac{1}, _inv{0} {}
    Comb(int n) : Comb() {
        init(n);
    }
    
    void init(int m) {
        m = std::min(m, Z::getMod() - 1);
        if (m <= n) return;
        _fac.resize(m + 1);
        _invfac.resize(m + 1);
        _inv.resize(m + 1);
        
        for (int i = n + 1; i <= m; i++) {
            _fac[i] = _fac[i - 1] * i;
        }
        _invfac[m] = _fac[m].inv();
        for (int i = m; i > n; i--) {
            _invfac[i - 1] = _invfac[i] * i;
            _inv[i] = _invfac[i] * _fac[i - 1];
        }
        n = m;
    }
    
    Z fac(int m) {
        if (m > n) init(2 * m);
        return _fac[m];
    }
    Z invfac(int m) {
        if (m > n) init(2 * m);
        return _invfac[m];
    }
    Z inv(int m) {
        if (m > n) init(2 * m);
        return _inv[m];
    }
    Z binom(int n, int m) {
        if (n < m || m < 0) return 0;
        return fac(n) * invfac(m) * invfac(n - m);
    }
} comb;
```



### n * n 行列式 计算

```c++
const int MAXN = 100;

int det(int a[MAXN][MAXN], int n) { 
    int res = 0;
    if (n == 1) {
        return a[0][0];
    } else {
        for (int j = 0; j < n; j++) {
            int t[MAXN][MAXN];
            for (int i = 1; i < n; i++) {
                int k = 0;
                for (int p = 0; p < n; p++) {
                    if (p == j) {
                        continue;
                    }
                    t[i - 1][k++] = a[i][p];
                }
            }
            res += ((j % 2 == 1) ? -1 : 1) * a[0][j] * det(t, n - 1);
        }
    }
    return res;
}
```

```c++
typedef long long LL;
long long get(long long n, long long k){ // 1 ~ n 中第 k 位上 1 的个数, 0 <= n, 0 <= k <= 62
    return (n + 1) / (1LL << k + 1) * (1LL << k) + max((n + 1) % (1LL << k + 1) - (1LL << k), 0LL);
}
```

### 差分约束spfa

```c++
bool spfa(int u,int n,std::vector< std::pair<int,int> > edge[N]) {
	std::vector<bool> vis(N,false);
	std::vector<int> num(N,0),dis(N,0x3f);
	std::queue<int> q; q.push(u);
	dis[u] = 0;  vis[u] = true;
	int count = 0;
	while(!q.empty()){
		int t = q.front();
		q.pop();
		vis[t] = false;
		for(int i = 0; i < edge[t].size(); i++) {
			auto [x,y] = edge[t][i];
			if(dis[x] > dis[t] + y) { // 最大值 最短路 最小值 最长路
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
```

### Dijsktra

```c++
struct node{
    int di;
    int pos;
    bool operator <(const node &x)const{
        return x.di < di;
    }
};
void Dijkstra(int u, std::vector< std::pair<int,int> > edge[N])
{
	 std::priority_queue<node> q;
     std::vector<int> dis(N,0x3f3f3f3f);
     std::vector<bool> vis(N,false);
     dis[u] = 0;
     q.push((node){0,u});
     while(!q.empty())
     {
         node p = q.top();
         q.pop();
         int x = p.pos;
         if(vis[x]) continue;
         vis[x] = 1;
         for(int i = 0; i < edge[x].size(); i++)
         {
            auto [y,z] = edge[x][i];
            if(dis[y] > dis[x] + z)
            {
               dis[y] = dis[x] + z;
               q.push((node){dis[y],y});
            }
         }
     }
}

```





### FFT  A* B 

```c++
#include <bits/stdc++.h>
typedef long long ll;

using namespace std;

const double PI = acos(-1.0);

// 递归实现FFT
void fft(vector<complex<double>>& a, bool inv) {
    int n = a.size();
    if (n == 1) {
        return;
    }
    
    //分治
    vector<complex<double>> a0(n / 2), a1(n / 2);
    for (int i = 0, j = 0; i < n; i += 2, j++) {
        a0[j] = a[i];
        a1[j] = a[i + 1];
    }
    fft(a0, inv);
    fft(a1, inv);
    
    //FFT
    double angle = 2 * PI / n * (inv ? -1 : 1);
    complex<double> w(1), wn(cos(angle), sin(angle));
    for (int i = 0; i < n / 2; i++) {
        a[i] = a0[i] + w * a1[i];
        a[i + n / 2] = a0[i] - w * a1[i];
        w *= wn;
    }
}

// FFT乘法
vector<int> multiply(vector<int> a, vector<int> b) {
    int n = 1;

    while (n < a.size() + b.size()) {
        n *= 2;
    }
    a.resize(n), b.resize(n);
    
    vector<complex<double>> c(n), d(n);
    for (int i = 0; i < n; i++) {
        c[i] = complex<double>(a[i], 0);
        d[i] = complex<double>(b[i], 0);
    }

    fft(c, false), fft(d, false);
    for (int i = 0; i < n; i++) {
        c[i] *= d[i];
    }

    fft(c, true);

    vector<int> res(n);
    for (int i = 0; i < n; i++) {
        res[i] = (int)(c[i].real() / n + 0.5);
    }

    int carry = 0;
    for (int i = 0; i< n; i++) {
    	res[i] += carry;
    	carry = res[i] / 10;
    	res[i] %= 10;
	}

	while (res.size() > 1 && res.back() == 0) {
    	res.pop_back();
	}
	return res;
}

vector<int> to_vector(string s) {
	vector<int> res;
	for (int i = s.size() - 1; i >= 0; i--) {
		res.push_back(s[i] - '0');
	}
	return res;
}

string to_string(vector<int> a) {
	string res;
	for (int i = a.size() - 1; i >= 0; i--) {
		res += to_string(a[i]);
	}
	return res;
}



void solve() {
	string s1, s2;
	cin >> s1 >> s2;
	vector<int> a = to_vector(s1), b = to_vector(s2);
	vector<int> c = multiply(a, b);
	cout << to_string(c) << '\n';
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

### 二分图最大匹配   匈牙利算法 $O(VE)$ 

```c++
bool find(int u) {  // 有向边
	for(int i = head[u]; i ; i = e[i].next) {
		int v = e[i].to;
		if(st[v] == 0) {
			st[v] = 1;
			if(match[v] == 0 || find(match[v]) == true) {
				match[v] = u;
				return true;
			}
		}
	}
	return false;
}
    
    for(int i = 1; i <= n; i ++){
        memset(st,0,sizeof(st)); 
        if(find(i)) ans++;
}
```

### 二分图染色与计数环

```c++
void dfs(int u) {
    vis[u] = true; // 无向边
	for(int i = head[u]; i ; i = e[i].next) {
		int v = e[i].to;
		if(vis[v] == false) {
			vis[v] = true;
			color[v] = !color[u];
			pre[v] = u;
			dfs(v);
		}
		else if(color[u] == color[v]) { // 输出奇数环
			int num = 1;
			for(int k = u; k != v; k = pre[k]) {
				num ++;
			}
			std::cout << num << '\n'; //奇数环长度
			for(int k = u; k != v; k = pre[k]) {
				std::cout << k << " ";
			}
			std::cout << v << '\n';
			exit(0);
		}
	}
}
```

### 矩阵乘法 & 快速幂

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

### Hash

```c++
const int p = 25165843;
const int N = 2e6 + 50;
const int mod = 2147483587;
typedef unsigned long long ull;
ull P[N],h[N];
ull _hash(int l,int r) {
	return (h[r] - h[l-1] * P[r - l + 1] % mod + mod) % mod;
}


	for(int i = 0; i < len; i ++) {
		h[i+1] = h[i] * p + (s[i] - '0');
		h[i+1] %= mod;
	}
	P[0] = 1;
	for(int i = 1; i <= 1e6 + 50; i ++) {
		P[i] = P[i-1] * p;
		P[i] %= mod;
	}
```

### 实数二分

```c++
while(l + 1e-5 < r) {
    double mid = (l + r) / 2.0;
    if(check(mid)) {
        l = mid;
    }
    else r = mid;
}
```

### 整数三分

```c++
ll l = 0, r = 1e10;
    ll ans = 1e14 + 7;
    while(r - l > 1) {
			ll mid = l + r >> 1;
			ll lmid = mid - 1;
			ll rmid = mid + 1;
			if(check(lmid) < check(rmid)) r = mid;  // check 要要求最大  将 < 改成 >
			else l = mid;
	}
    //std::cout << l << ' ' << r << '\n';
	ans = std::min({ans,check(l),check(r)});
```



### Dijkstra

```c++
struct node{
    int dis;
    int pos;
    bool operator <(const node &x) const {
        return x.dis < dis;
    }
};


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
    };
```

### 建边 与 重建边

```c++
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

    for(int i = 0; i <= cnt; i ++) {
        e[i] = {0,0,0};
    }   std::memset(head,0,sizeof(head)); cnt = 0;
```

### $RMQ$  区间最大值

```c++
int f[N][30];


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
```

### Z 函数

对于一个长度为$n$的字符串$s$,$z[i]$ 表示$s$与其后缀$s[i,n]$ 的最长公共前缀($Lcp$)的长度

```c++
std::vector<int> Z(std::string s) {
    int n = s.size();
    std::vector<int> z(n + 1);
    z[0] = n;
    for (int i = 1, j = 1; i < n; i++) {
        z[i] = std::max(0, std::min(j + z[j] - i, z[i - j]));
        while (i + z[i] < n && s[z[i]] == s[i + z[i]]) {
            z[i]++;
        }
        if (i + z[i] > j + z[j]) {
            j = i;
        }
    }
    return z;
}
// t 与 s的每一个后缀的 LCP 长度数组 
std::vector<int> exkmp(std::string s, std::string t) {
    std::string st = t + "$" + s;
    std::vector<int> z = Z(st);
    std::vector<int> ans(z.size() - t.size() - 1);
    for (int i = t.size() + 1; i < z.size(); i++) {
        ans[i - t.size() - 1] = z[i];
    }
    return ans;
}
```

1. 给出模式串$p$,文本串$s$, 求$p$在$s$中 的所有出现位置。 $st$的  $Z[i+|p| + 1] = |p|$  对应一次出现

2. 求$s$的所有border ， 如果$i + Z(i) = |s|$  说明这个$Z-Box$是个border （既是前缀也是后缀）

   ### manacher

   **预处理字符串**：在原字符串`s`的每个字符之间插入特殊字符（如`#`），并在字符串的开头和结尾也插入特殊字符。这样，所有的回文子串（无论是奇数长度还是偶数长度）都会被统一处理。 将新字符串转换为整数串。

   ```c++
   std::vector<int> manacher(std::vector<int> s) {
       std::vector<int> t{0};
       for (auto c : s) {
           t.push_back(c);
           t.push_back(0);
       }
       int n = t.size();
       std::vector<int> r(n);
       for (int i = 0, j = 0; i < n; i++) {
           if (2 * j - i >= 0 && j + r[j] > i) {
               r[i] = std::min(r[2 * j - i], j + r[j] - i);
           }
           while (i - r[i] >= 0 && i + r[i] < n && t[i - r[i]] == t[i + r[i]]) {
               r[i] += 1;
           }
           if (i + r[i] > j + r[j]) {
               j = i;
           }
       }
       return r;
   }
   ```

   遍历结束后，`r`中存储了以每个字符为中心的最长回文子串的半径。最长回文子串的长度即为`max(r)` - 1。（因为加了新字符）
   
   ### 素数测试与因式分解（Miller-Rabin & Pollard-Rho）
   
   ```c++
   i64 mul(i64 a, i64 b, i64 m) {
       return static_cast<__int128>(a) * b % m;
   }
   i64 power(i64 a, i64 b, i64 m) {
       i64 res = 1 % m;
       for (; b; b >>= 1, a = mul(a, a, m))
           if (b & 1)
               res = mul(res, a, m);
       return res;
   }
   bool isprime(i64 n) {
       if (n < 2)
           return false;
       static constexpr int A[] = {2, 3, 5, 7, 11, 13, 17, 19, 23};
       int s = __builtin_ctzll(n - 1);
       i64 d = (n - 1) >> s;
       for (auto a : A) {
           if (a == n)
               return true;
           i64 x = power(a, d, n);
           if (x == 1 || x == n - 1)
               continue;
           bool ok = false;
           for (int i = 0; i < s - 1; ++i) {
               x = mul(x, x, n);
               if (x == n - 1) {
                   ok = true;
                   break;
               }
           }
           if (!ok)
               return false;
       }
       return true;
   }
   std::vector<i64> factorize(i64 n) {
       std::vector<i64> p;
       std::function<void(i64)> f = [&](i64 n) {
           if (n <= 10000) {
               for (int i = 2; i * i <= n; ++i)
                   for (; n % i == 0; n /= i)
                       p.push_back(i);
               if (n > 1)
                   p.push_back(n);
               return;
           }
           if (isprime(n)) {
               p.push_back(n);
               return;
           }
           auto g = [&](i64 x) {
               return (mul(x, x, n) + 1) % n;
           };
           i64 x0 = 2;
           while (true) {
               i64 x = x0;
               i64 y = x0;
               i64 d = 1;
               i64 power = 1, lam = 0;
               i64 v = 1;
               while (d == 1) {
                   y = g(y);
                   ++lam;
                   v = mul(v, std::abs(x - y), n);
                   if (lam % 127 == 0) {
                       d = std::gcd(v, n);
                       v = 1;
                   }
                   if (power == lam) {
                       x = y;
                       power *= 2;
                       lam = 0;
                       d = std::gcd(v, n);
                       v = 1;
                   }
               }
               if (d != n) {
                   f(d);
                   f(n / d);
                   return;
               }
               ++x0;
           }
       };
       f(n);
       std::sort(p.begin(), p.end());
       return p;
   }
   ```
   
   
   
   ### 线性筛素数
   
   ```c++
   	for(int i = 2;i < N; i++) {
       	if(not_prime[i] == 0) plist[++cnt] = i;
       	for(int j = 1;j <= cnt;j++)
       	{
           	int x;
           	x = i * plist[j];
           	if(x > N) break;
           	not_prime[x] = 1;
           	if(i % plist[j] == 0) break;
       	}
   	}
   ```
   
   ###   小波树
   
   静态数据结构
   
   区间第k小
   
   区间某个数出现的频率。
   
   区间小于等于某个数的个数
   
   ```c++
   struct BitRank {
       // block 管理一行一行的bit
       std::vector<unsigned long long> block;
       std::vector<unsigned int> count;
       BitRank() {}
       // 位向量长度
       void resize(const unsigned int num) {
           block.resize(((num + 1) >> 6) + 1, 0);
           count.resize(block.size(), 0);
       }
       // 设置i位bit
       void set(const unsigned int i, const unsigned long long val) {
           block[i >> 6] |= (val << (i & 63));
       }
       void build() {
           for (unsigned int i = 1; i < block.size(); i++) {
               count[i] = count[i - 1] + __builtin_popcountll(block[i - 1]);
           }
       }
       // [0, i) 1的个数
       unsigned int rank1(const unsigned int i) const {
           return count[i >> 6] +
               __builtin_popcountll(block[i >> 6] & ((1ULL << (i & 63)) - 1ULL));
       }
       // [i, j) 1的个数
       unsigned int rank1(const unsigned int i, const unsigned int j) const {
           return rank1(j) - rank1(i);
       }
       // [0, i) 0的个数
       unsigned int rank0(const unsigned int i) const { return i - rank1(i); }
       // [i, j) 0的个数
       unsigned int rank0(const unsigned int i, const unsigned int j) const {
           return rank0(j) - rank0(i);
       }
   };
   
   
   class WaveletMatrix {
   private:
       unsigned int height;
       std::vector<BitRank> B;
       std::vector<int> pos;
   
   public:
       WaveletMatrix() {}
       WaveletMatrix(std::vector<int> vec)
           : WaveletMatrix(vec, *std::max_element(vec.begin(), vec.end()) + 1) {}
       // sigma: 字母表大小(字符串的话)，数字序列的话是数的种类
       WaveletMatrix(std::vector<int> vec, const unsigned int sigma) {
           init(vec, sigma);
       }
       void init(std::vector<int>& vec, const unsigned int sigma) {
           height = (sigma == 1) ? 1 : (64 - __builtin_clzll(sigma - 1));
           B.resize(height), pos.resize(height);
           for (unsigned int i = 0; i < height; ++i) {
               B[i].resize(vec.size());
               for (unsigned int j = 0; j < vec.size(); ++j) {
                   B[i].set(j, get(vec[j], height - i - 1));
               }
               B[i].build();
               auto it = stable_partition(vec.begin(), vec.end(), [&](int c) {
                   return !get(c, height - i - 1);
               });
               pos[i] = it - vec.begin();
           }
       }
   
       int get(const int val, const int i) { return val >> i & 1; }
       // [l, r) 中val出现的频率
   
       int rank(const int val, const int l, const int r) {
           return rank(val, r) - rank(val, l);
       }
       // [0, i) 中val出现的频率
       int rank(int val, int i) {
           int p = 0;
           for (unsigned int j = 0; j < height; ++j) {
               if (get(val, height - j - 1)) {
                   p = pos[j] + B[j].rank1(p);
                   i = pos[j] + B[j].rank1(i);
               } else {
                   p = B[j].rank0(p);
                   i = B[j].rank0(i);
               }
           }
           return i - p;
       }
       // [l, r) 中k小  找区间第三小就是 封装第二小 返回的是值
       int quantile(int k, int l, int r) {
           int res = 0;
           for (unsigned int i = 0; i < height; ++i) {
               const int j = B[i].rank0(l, r);
               if (j > k) {
                   l = B[i].rank0(l);
                   r = B[i].rank0(r);
               } else {
                   l = pos[i] + B[i].rank1(l);
                   r = pos[i] + B[i].rank1(r);
                   k -= j;
                   res |= (1 << (height - i - 1));
               }
           }
           return res;
       }
       int rangefreq(const int i, const int j, const int a, const int b, const int l,
                     const int r, const int x) {
           if (i == j || r <= a || b <= l) return 0;
           const int mid = (l + r) >> 1;
           if (a <= l && r <= b) {
               return j - i;
           } else {
               const int left =
                   rangefreq(B[x].rank0(i), B[x].rank0(j), a, b, l, mid, x + 1);
               const int right = rangefreq(pos[x] + B[x].rank1(i),
                                           pos[x] + B[x].rank1(j), a, b, mid, r, x + 1);
               return left + right;
           }
       }
       // [l,r) 在[a, b) 值域的数字个数
       int rangefreq(const int l, const int r, const int a, const int b) {
           return rangefreq(l, r, a, b, 0, 1 << height, 0);
       }
       int rangemin(const int i, const int j, const int a, const int b, const int l,
                    const int r, const int x, const int val) {
           if (i == j || r <= a || b <= l) return -1;
           if (r - l == 1) return val;
           const int mid = (l + r) >> 1;
           const int res =
               rangemin(B[x].rank0(i), B[x].rank0(j), a, b, l, mid, x + 1, val);
           if (res < 0)
               return rangemin(pos[x] + B[x].rank1(i), pos[x] + B[x].rank1(j), a, b, mid,
                               r, x + 1, val + (1 << (height - x - 1)));
           else
               return res;
       }
       // [l,r) 在[a,b) 值域内存在的最小值是什么，不存在返回-1
       int rangemin(int l, int r, int a, int b) {
           return rangemin(l, r, a, b, 0, 1 << height, 0, 0);
       }
   };
   
   WaveletMatrix T(a);
   ```
   
   ### O(n) 区间每个数的约数个数
   
   ```c++
   int f[N + 1],cnt[N + 1],prime[N + 1];	
   	for(int i = 2; i < N; i++) {
   		if(prime[i] == 0) {
   			prime[ ++prime[0] ] = i;
   			f[i] = 2; // 约数个数
   			cnt[i] = 1; //i中prime[j]的次数
   		}
   		for(int j = 1; j <= prime[0]; j++) {
   			if(prime[j] * i > N) break;
   			prime[ prime[j] * i ] = 1;
   			if(i % prime[j] == 0) {
   				f[ prime[j] * i ] = f[i] / (cnt[i] + 1) * (cnt[i] + 2); // 不互质
   				cnt[ prime[j] * i ] = cnt[i] + 1;
   				break;
   			}
   			else {
   				f[ prime[j] * i ] = f[prime[j]] * f[i]; // 互质
   				cnt[ prime[j] * i ] = 1; 
   			}
   		}
   	}
   ```
   
   ### 大于 x 的最小二的幂次
   
   ```c++
   i64 NPT(i64 x) {
       if (x <= 0) return 1;
       // 如果 x 已经是二的幂次，直接返回 x
       if ((x & (x - 1)) == 0) return x;
       // 找到大于 x 的最小二的幂次
       int h_bit = 63 - __builtin_clzll(x); // 使用 GCC/Clang 内置函数
       i64 res = 1LL << (h_bit + 1);
       // 如果结果超出了 long long 的范围，返回 -1 作为错误信号
       if (res < 0) return -1;
       return res;
   }
   ```
   
   ### 归并排序
   
   ```c++
   i64 msort(std::vector<int> &a,int l,int r)
   {
       if(l >= r) return 0;
       int mid = (l + r) / 2;
       msort(a,l,mid); 
       msort(a,mid+1,r);
       int i = l, j = mid + 1,k = l;
       while(i <= mid && j <= r)
       {
           if(a[i] <= a[j])  b[k++] = a[i++];
           else {
               b[k++] = a[j++];
               ans += (mid - i + 1);
           }
       }
       while(i <= mid) b[k++] = a[i++];
       while(j <= r) b[k++] = a[j++];
       for(int i = l; i <= r; i++)  a[i] = b[i];
   	return ans;
   }
   ```
   
   
