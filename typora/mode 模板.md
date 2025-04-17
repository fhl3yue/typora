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

### 火车头

```
#pragma GCC optimize(3)
#pragma GCC target("avx")
#pragma GCC optimize("Ofast")
#pragma GCC optimize("inline")
#pragma GCC optimize("-fgcse")
#pragma GCC optimize("-fgcse-lm")
#pragma GCC optimize("-fipa-sra")
#pragma GCC optimize("-ftree-pre")
#pragma GCC optimize("-ftree-vrp")
#pragma GCC optimize("-fpeephole2")
#pragma GCC optimize("-ffast-math")
#pragma GCC optimize("-fsched-spec")
#pragma GCC optimize("unroll-loops")
#pragma GCC optimize("-falign-jumps")
#pragma GCC optimize("-falign-loops")
#pragma GCC optimize("-falign-labels")
#pragma GCC optimize("-fdevirtualize")
#pragma GCC optimize("-fcaller-saves")
#pragma GCC optimize("-fcrossjumping")
#pragma GCC optimize("-fthread-jumps")
#pragma GCC optimize("-funroll-loops")
#pragma GCC optimize("-fwhole-program")
#pragma GCC optimize("-freorder-blocks")
#pragma GCC optimize("-fschedule-insns")
#pragma GCC optimize("inline-functions")
#pragma GCC optimize("-ftree-tail-merge")
#pragma GCC optimize("-fschedule-insns2")
#pragma GCC optimize("-fstrict-aliasing")
#pragma GCC optimize("-fstrict-overflow")
#pragma GCC optimize("-falign-functions")
#pragma GCC optimize("-fcse-skip-blocks")
#pragma GCC optimize("-fcse-follow-jumps")
#pragma GCC optimize("-fsched-interblock")
#pragma GCC optimize("-fpartial-inlining")
#pragma GCC optimize("no-stack-protector")
#pragma GCC optimize("-freorder-functions")
#pragma GCC optimize("-findirect-inlining")
#pragma GCC optimize("-fhoist-adjacent-loads")
#pragma GCC optimize("-frerun-cse-after-loop")
#pragma GCC optimize("inline-small-functions")
#pragma GCC optimize("-finline-small-functions")
#pragma GCC optimize("-ftree-switch-conversion")
#pragma GCC optimize("-foptimize-sibling-calls")
#pragma GCC optimize("-fexpensive-optimizations")
#pragma GCC optimize("-funsafe-loop-optimizations")
#pragma GCC optimize("inline-functions-called-once")
#pragma GCC optimize("-fdelete-null-pointer-checks")
#pragma GCC optimize(2)
```

### 初始

```
#include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
using i64 = long long;
using i128 = __int128;
const int N = 2e3 + 4;
const int mod = 1e9 + 7;
//vector<vector<bool>> vis(n, vector<bool>(m, false));
void solve() {


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

### 随机数生成

```
#include <random>

    random_device rd;  // 随机数生成器
    mt19937_64 rng(rd());  // 基于 Mersenne Twister 的64位随机数生成器
    uniform_int_distribution<ll> dist(2LL, 1000000000000000000LL);  // 随机数范围
    ll x = dist(rng);
```

### string

```
class STR {
public:
    std::string s;
    int len;

    STR(std::string st) {
        s = st; // 初始化成员变量 s
        len = st.length();
    }

    std::vector<int> strInt(const std::string &input) { // 提取字符串中所有数字
        std::vector<int> num;
        std::regex integerRegex("-?\\d+");
        std::sregex_iterator it(input.begin(), input.end(), integerRegex);
        std::sregex_iterator end;

        while (it != end) {
            num.push_back(std::stoi(it->str()));
            ++it;
        }
        return num;
    }

    bool issub(std::string o) { // 判定字串
        std::string::size_type idx = s.find(o);
        if (idx == std::string::npos) return false;
        else return true;
    }

    std::string str(int i, int j) {
        return s.substr(i, j);
    }

    int query(std::string a) { // 统计不重叠的子串数量
        int count = 0;
        std::string::size_type idx = s.find(a);
        while (idx != std::string::npos) {
            ++count;
            idx = s.find(a, idx + a.length());
        }
        return count;
    }

    std::pair<int, std::string> lowper(int id) {
        if (id == 1) { // 大写统计和转换
            int d = std::count_if(s.begin(), s.end(), ::isupper);
            std::string dx = s;
            std::transform(dx.begin(), dx.end(), dx.begin(), ::toupper); // 转换为大写
            return {d, dx};
        } else { // 小写统计和转换
            int x = std::count_if(s.begin(), s.end(), ::islower);
            std::string xx = s;
            std::transform(xx.begin(), xx.end(), xx.begin(), ::tolower); // 转换为小写
            return {x, xx};
        }
    }
};
```

### 取模 

```c++
using i64 = long long;
using u64 = unsigned long long;
using u32 = unsigned;
using u128 = unsigned __int128;

template<class T>
constexpr T power(T a, u64 b, T res = 1) {
    for (; b != 0; b /= 2, a *= a) {
        if (b & 1) {
            res *= a;
        }
    }
    return res;
}

template<u32 P>
constexpr u32 mulMod(u32 a, u32 b) {
    return u64(a) * b % P;
}

template<u64 P>
constexpr u64 mulMod(u64 a, u64 b) {
    u64 res = a * b - u64(1.L * a * b / P - 0.5L) * P;
    res %= P;
    return res;
}

constexpr i64 safeMod(i64 x, i64 m) {
    x %= m;
    if (x < 0) {
        x += m;
    }
    return x;
}

constexpr std::pair<i64, i64> invGcd(i64 a, i64 b) {
    a = safeMod(a, b);
    if (a == 0) {
        return {b, 0};
    }
    
    i64 s = b, t = a;
    i64 m0 = 0, m1 = 1;

    while (t) {
        i64 u = s / t;
        s -= t * u;
        m0 -= m1 * u;
        
        std::swap(s, t);
        std::swap(m0, m1);
    }
    
    if (m0 < 0) {
        m0 += b / s;
    }
    
    return {s, m0};
}

template<std::unsigned_integral U, U P>
struct ModIntBase {
public:
    constexpr ModIntBase() : x(0) {}
    template<std::unsigned_integral T>
    constexpr ModIntBase(T x_) : x(x_ % mod()) {}
    template<std::signed_integral T>
    constexpr ModIntBase(T x_) {
        using S = std::make_signed_t<U>;
        S v = x_ % S(mod());
        if (v < 0) {
            v += mod();
        }
        x = v;
    }
    
    constexpr static U mod() {
        return P;
    }
    
    constexpr U val() const {
        return x;
    }
    
    constexpr ModIntBase operator-() const {
        ModIntBase res;
        res.x = (x == 0 ? 0 : mod() - x);
        return res;
    }
    
    constexpr ModIntBase inv() const {
        return power(*this, mod() - 2);
    }
    
    constexpr ModIntBase &operator*=(const ModIntBase &rhs) & {
        x = mulMod<mod()>(x, rhs.val());
        return *this;
    }
    constexpr ModIntBase &operator+=(const ModIntBase &rhs) & {
        x += rhs.val();
        if (x >= mod()) {
            x -= mod();
        }
        return *this;
    }
    constexpr ModIntBase &operator-=(const ModIntBase &rhs) & {
        x -= rhs.val();
        if (x >= mod()) {
            x += mod();
        }
        return *this;
    }
    constexpr ModIntBase &operator/=(const ModIntBase &rhs) & {
        return *this *= rhs.inv();
    }
    
    friend constexpr ModIntBase operator*(ModIntBase lhs, const ModIntBase &rhs) {
        lhs *= rhs;
        return lhs;
    }
    friend constexpr ModIntBase operator+(ModIntBase lhs, const ModIntBase &rhs) {
        lhs += rhs;
        return lhs;
    }
    friend constexpr ModIntBase operator-(ModIntBase lhs, const ModIntBase &rhs) {
        lhs -= rhs;
        return lhs;
    }
    friend constexpr ModIntBase operator/(ModIntBase lhs, const ModIntBase &rhs) {
        lhs /= rhs;
        return lhs;
    }
    
    friend constexpr std::istream &operator>>(std::istream &is, ModIntBase &a) {
        i64 i;
        is >> i;
        a = i;
        return is;
    }
    friend constexpr std::ostream &operator<<(std::ostream &os, const ModIntBase &a) {
        return os << a.val();
    }
    
    friend constexpr bool operator==(const ModIntBase &lhs, const ModIntBase &rhs) {
        return lhs.val() == rhs.val();
    }
    friend constexpr std::strong_ordering operator<=>(const ModIntBase &lhs, const ModIntBase &rhs) {
        return lhs.val() <=> rhs.val();
    }
    
private:
    U x;
};

template<u32 P>
using ModInt = ModIntBase<u32, P>;
template<u64 P>
using ModInt64 = ModIntBase<u64, P>;

struct Barrett {
public:
    Barrett(u32 m_) : m(m_), im((u64)(-1) / m_ + 1) {}

    constexpr u32 mod() const {
        return m;
    }

    constexpr u32 mul(u32 a, u32 b) const {
        u64 z = a;
        z *= b;
        
        u64 x = u64((u128(z) * im) >> 64);
        
        u32 v = u32(z - x * m);
        if (m <= v) {
            v += m;
        }
        return v;
    }

private:
    u32 m;
    u64 im;
};

template<u32 Id>
struct DynModInt {
public:
    constexpr DynModInt() : x(0) {}
    template<std::unsigned_integral T>
    constexpr DynModInt(T x_) : x(x_ % mod()) {}
    template<std::signed_integral T>
    constexpr DynModInt(T x_) {
        int v = x_ % int(mod());
        if (v < 0) {
            v += mod();
        }
        x = v;
    }
    
    constexpr static void setMod(u32 m) {
        bt = m;
    }
    
    static u32 mod() {
        return bt.mod();
    }
    
    constexpr u32 val() const {
        return x;
    }
    
    constexpr DynModInt operator-() const {
        DynModInt res;
        res.x = (x == 0 ? 0 : mod() - x);
        return res;
    }
    
    constexpr DynModInt inv() const {
        auto v = invGcd(x, mod());
        assert(v.first == 1);
        return v.second;
    }
    
    constexpr DynModInt &operator*=(const DynModInt &rhs) & {
        x = bt.mul(x, rhs.val());
        return *this;
    }
    constexpr DynModInt &operator+=(const DynModInt &rhs) & {
        x += rhs.val();
        if (x >= mod()) {
            x -= mod();
        }
        return *this;
    }
    constexpr DynModInt &operator-=(const DynModInt &rhs) & {
        x -= rhs.val();
        if (x >= mod()) {
            x += mod();
        }
        return *this;
    }
    constexpr DynModInt &operator/=(const DynModInt &rhs) & {
        return *this *= rhs.inv();
    }
    
    friend constexpr DynModInt operator*(DynModInt lhs, const DynModInt &rhs) {
        lhs *= rhs;
        return lhs;
    }
    friend constexpr DynModInt operator+(DynModInt lhs, const DynModInt &rhs) {
        lhs += rhs;
        return lhs;
    }
    friend constexpr DynModInt operator-(DynModInt lhs, const DynModInt &rhs) {
        lhs -= rhs;
        return lhs;
    }
    friend constexpr DynModInt operator/(DynModInt lhs, const DynModInt &rhs) {
        lhs /= rhs;
        return lhs;
    }
    
    friend constexpr std::istream &operator>>(std::istream &is, DynModInt &a) {
        i64 i;
        is >> i;
        a = i;
        return is;
    }
    friend constexpr std::ostream &operator<<(std::ostream &os, const DynModInt &a) {
        return os << a.val();
    }
    
    friend constexpr bool operator==(const DynModInt &lhs, const DynModInt &rhs) {
        return lhs.val() == rhs.val();
    }
    friend constexpr std::strong_ordering operator<=>(const DynModInt &lhs, const DynModInt &rhs) {
        return lhs.val() <=> rhs.val();
    }
    
private:
    u32 x;
    static Barrett bt;
};

template<u32 Id>
Barrett DynModInt<Id>::bt = 998244353;

using Z = ModInt<998244353>;
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
template<typename T = int>
struct Graph {
    int n;
    vector<vector<pair<int, T>>> adj;
    Graph(int n): n(n), adj(n) {}
    void addEdge(int u, int v, T w) { adj[u].push_back({v, w}); }
    vector<T> dijkstra(int s) {
        const T INF = numeric_limits<T>::max();
        vector<T> dis(n, INF);
        priority_queue<pair<T,int>, vector<pair<T,int>>, greater<pair<T,int>>> pq;
        dis[s] = 0; pq.push({0, s});
        while(!pq.empty()){
            auto [d,u] = pq.top(); pq.pop();
            if(d > dis[u]) continue;
            for(auto &p : adj[u]) {
                int v = p.first; T w = p.second;
                if(dis[v] > d + w) {
                    dis[v] = d + w;
                    pq.push({dis[v], v});
                }
            }
        }
        return dis;
    }
};
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

###  tarjan 缩点

```
class Tarjan {
public:
    struct Edge { int u, v; };
    // mode: 0=SCC, 1=割点, 2=桥, 3=边双连通分量
    Tarjan(int n, int mode = 0) : n(n), mode(mode) {
        G.resize(n + 1);
        dfn.assign(n + 1, 0);
        low.assign(n + 1, 0);
        tm = 0; sccC = 0;
        if(mode == 0) {
            vis.assign(n + 1, false);
            comp.assign(n + 1, 0);
            sccS.assign(n + 1, 0);
            sccN.resize(n + 1);
            sccM.assign(n + 1, n + 1);
        } else if(mode == 1 || mode == 2) {
            cut.assign(n + 1, false);
        }
    }

    void addEdge(int u, int v) {
        if(mode == 3) {
            int id = E.size();
            E.push_back({u, v});
            G[u].push_back(id);
            if(u != v) G[v].push_back(id);
        } else {
            G[u].push_back(v);
            if(mode > 0)
                G[v].push_back(u);
        }
    }

    void run() {
        if(mode == 3) {
            isBr.assign(E.size(), false);
            for (int i = 1; i <= n; i++) {
                if (!dfn[i]) dfsEB(i, -1);
            }
            vector<vector<int>> newG(n + 1);
            for (int i = 0; i < (int)E.size(); i++){
                if (!isBr[i]) {
                    int u = E[i].u, v = E[i].v;
                    newG[u].push_back(v);
                    if(u != v) newG[v].push_back(u);
                }
            }
            ebccC.assign(n + 1, -1);
            int cid = 0;
            function<void(int, int)> dfsC = [&](int u, int c) {
                ebccC[u] = c;
                for (int nxt : newG[u])
                    if (ebccC[nxt] == -1) dfsC(nxt, c);
            };
            for (int i = 1; i <= n; i++) {
                if (ebccC[i] == -1) dfsC(i, cid++);
            }
            ebcc.resize(cid);
            ebccCnt = cid;
            for (int i = 1; i <= n; i++) {
                ebcc[ ebccC[i] ].push_back(i);
            }
            for (auto &c : ebcc)
                sort(c.begin(), c.end());
        } else {
            for (int i = 1; i <= n; i++) {
                if (!dfn[i]) {
                    if (mode == 0)
                        sccDFS(i);
                    else
                        undDFS(i, -1);
                }
            }
            if (mode == 2)
                sort(br.begin(), br.end());
        }
    }

    // SCC接口 (mode==0)
    int getSccCount() const { return sccC; }
    const vector<int>& getComp() const { return comp; }
    const vector<int>& getSccSize() const { return sccS; }
    const vector<vector<int>>& getSccNodes() const { return sccN; }
    const vector<int>& getSccMin() const { return sccM; }

    const vector<bool>& getCut() const { return cut; }
    const vector<pair<int,int>>& getBridges() const { return br; }

    int getEbccCount() const { return ebccCnt; }
    const vector<vector<int>>& getEbcc() const { return ebcc; }
private:
    int n, mode;
    vector<vector<int>> G;
    vector<int> dfn, low;
    int tm, sccC;

    vector<bool> vis;
    vector<int> comp, sccS, sccM;
    vector<vector<int>> sccN;
    stack<int> st;

    vector<bool> cut;
    vector<pair<int,int>> br;

    vector<Edge> E;
    vector<bool> isBr;
    vector<int> ebccC;
    vector<vector<int>> ebcc;
    int ebccCnt;

    void sccDFS(int u) {
        dfn[u] = low[u] = ++tm;
        st.push(u); vis[u] = true;
        for (int v : G[u]) {
            if (!dfn[v]) {
                sccDFS(v);
                low[u] = min(low[u], low[v]);
            } else if (vis[v]) {
                low[u] = min(low[u], dfn[v]);
            }
        }
        if (dfn[u] == low[u]) {
            sccC++;
            vector<int> compNodes;
            int mini = u;
            while (true) {
                int cur = st.top(); st.pop();
                vis[cur] = false;
                comp[cur] = sccC;
                compNodes.push_back(cur);
                mini = min(mini, cur);
                if(cur == u) break;
            }
            sccS[sccC] = compNodes.size();
            sccN[sccC] = compNodes;
            sccM[sccC] = mini;
        }
    }

    void undDFS(int u, int par) {
        dfn[u] = low[u] = ++tm;
        int child = 0;
        for (int v : G[u]) {
            if(v == par) continue;
            if (!dfn[v]) {
                child++;
                undDFS(v, u);
                low[u] = min(low[u], low[v]);
                if (mode == 1) {
                    if (par == -1 && child > 1) cut[u] = true;
                    if (par != -1 && low[v] >= dfn[u]) cut[u] = true;
                }
                if (mode == 2 && low[v] > dfn[u])
                    br.push_back({min(u, v), max(u, v)});
            } else {
                low[u] = min(low[u], dfn[v]);
            }
        }
    }

    void dfsEB(int u, int pe) {
        dfn[u] = low[u] = ++tm;
        for (int eid : G[u]) {
            if (eid == pe) continue;
            int v = (E[eid].u == u ? E[eid].v : E[eid].u);
            if (!dfn[v]) {
                dfsEB(v, eid);
                low[u] = min(low[u], low[v]);
                if (low[v] > dfn[u])
                    isBr[eid] = true;
            } else {
                low[u] = min(low[u], dfn[v]);
            }
        }
    }
};

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

### 实数三分 

```
const double eps = 1e-8;
double l = 0, r = 2e9, mid1, mid2;
    while (r - l > eps) {
        mid1 = l + (r - l) / 3.0;
        mid2 = r - (r - l) / 3.0;
        if (f(mid1) > f(mid2)) l = mid1;// 单峰函数最小值
        else r = mid2;
    }

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
template<typename T, typename Binary = std::function<T(const T&, const T&)>>
class ST { // 1-index
private:
    std::vector<std::vector<T>> f;
    std::vector<int> Log;
    int n;
    Binary op;
    void buildLog() {
        Log[1] = 0;
        Log[2] = 1;
        for(int i = 3; i <= n; i++) {
            Log[i] = Log[i/2] + 1;
        }
    }
public:
    ST(const std::vector<T>& arr, Binary operation = std::max<T>)
        : n(arr.size() - 1), op(operation) {
        Log.resize(n + 1);
        buildLog();
        f.resize(n + 1, std::vector<T>(Log[n] + 1));
        for(int i = 1; i <= n; i++) {
            f[i][0] = arr[i];
        }
        for(int j = 1; j <= Log[n]; j++) {
            for(int i = 1; i + (1 << j) - 1 <= n; i++) {
                f[i][j] = op(f[i][j-1], f[i + (1 << (j-1))][j-1]);
            }
        }
    }
    T query(int l, int r) const {
        int p = Log[r - l + 1];
        return op(f[l][p], f[r - (1 << p) + 1][p]);
    }
};
//ST<i64> st(a, [](const i64& a, const i64& b) { return std::max(a, b); });
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

   ### 大数 分解出 因子

   ```c++
   i128 mul(i128 a, i128 b, i128 m) {
       return (__int128)a * b % m;
   }
   
   
   i128 power(i128 a, i128 n, i128 mod) {
       i128 res = 1;
       while (n) {
           if (n & 1) res = mul(res, a, mod);
           a = mul(a, a, mod);
           n >>= 1;
       }
       return res;
   }
   
   
   bool miller_rabin(i64 n) {
       if (n < 2) return false;
       if (n == 2) return true;
       if (n % 2 == 0) return false;
       
       i64 d = n - 1;
       int s = 0;
       while (d % 2 == 0) {
           d /= 2;
           s++;
       }
       for (int a : {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37}) {
           if (n == a) return true;
           if (n % a == 0) return false;
           
           i128 t = d;
           i128 y = power(a, t, n);
           while (t != n-1 && y != 1 && y != n-1) {
               y = mul(y, y, n);
               t *= 2;
           }
           if (y != n-1 && t % 2 == 0) return false;
       }
       return true;
   }
   
   i64 pollard_rho(i64 n) {  // O(n^(1/4))
       if (n == 1) return n;
       if (n % 2 == 0) return 2;
       if (miller_rabin(n)) return n;
       
       auto f = [n](i128 x) -> i128 { 
           return (mul(x, x, n) + rand() % (n-1) + 1) % n;
       };
       
       i128 x = rand() % (n-1) + 1;
       i128 y = x;
       i128 prd = 1;
       i64 i = 0, k = 2;
       
       while (true) {
           i++;
           x = f(x);
           prd = mul(prd, abs(y - x), n);
           
           if (i == k || prd == 0) {
               if (prd) {
                   i64 d = __gcd((i64)prd, n);
                   if (d != 1) return d;
               }
               if (i == k) {
                   y = x;
                   k *= 2;
               }
           }
           
           if (i > 1000000) {
               i64 d = __gcd((i64)abs(y - x), n);
               if (d > 1 && d < n) return d;
               x = rand() % (n-1) + 1;
               y = x;
               i = 0;
               k = 2;
               prd = 1;
           }
       }
   }
   
   void factorize(i64 n, vector<i64>& factors) {  
       if (n == 1) return;
       if (miller_rabin(n)) {
           factors.push_back(n);
           return;
       }
       i64 d = pollard_rho(n);
       factorize(d, factors);
       factorize(n/d, factors);
   }
   vector<i64> Fget(const vector<i64>& pro) {  //dlogd  所有因子
       unordered_map<i64, int> count;
       for(auto x : pro) {
           count[x]++;
       }
       vector<i64> factors = {1};
       for(auto [prime, cnt] : count) {
           int size = factors.size();
           i64 mul = 1;
           for(int i = 0; i < cnt; i++) {
               mul *= prime;
               for(int j = 0; j < size; j++) {
                   factors.push_back(factors[j] * mul);
               }
           }
       }
       sort(factors.begin(), factors.end());
       return factors;
   }
   ```

   

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
    // 64 位块存储位向量
    vector<unsigned long long> block;
    vector<unsigned int> count;
    
    BitRank() {}
    
    // 分配 block 与 count：num 表示位向量长度
    void resize(const unsigned int num) {
        block.resize(((num + 1) >> 6) + 1, 0);
        count.resize(block.size(), 0);
    }
    
    // 设置第 i 位为 val（通常为 0 或 1）
    void set(const unsigned int i, const unsigned long long val) {
        block[i >> 6] |= (val << (i & 63));
    }
    
    // 构建前缀和数组 count，用于快速查询
    void build() {
        for (unsigned int i = 1; i < block.size(); i++) {
            count[i] = count[i - 1] + __builtin_popcountll(block[i - 1]);
        }
    }
    
    // 查询 [0, i) 内 1 的个数
    unsigned int rank1(const unsigned int i) const {
        return count[i >> 6] +
            __builtin_popcountll(block[i >> 6] & ((1ULL << (i & 63)) - 1ULL));
    }
    
    // 查询 [i, j) 内 1 的个数
    unsigned int rank1(const unsigned int i, const unsigned int j) const {
        return rank1(j) - rank1(i);
    }
    
    // 查询 [0, i) 内 0 的个数
    unsigned int rank0(const unsigned int i) const { 
        return i - rank1(i); 
    }
    
    // 查询 [i, j) 内 0 的个数
    unsigned int rank0(const unsigned int i, const unsigned int j) const {
        return rank0(j) - rank0(i);
    }
};

template<class T>
class WaveletMatrix {
private:
    unsigned int height;     
    vector<BitRank> B;           
    vector<int> pos;            
public:
    WaveletMatrix() {}
    WaveletMatrix(const vector<T>& vec)
        : WaveletMatrix(vec, *max_element(vec.begin(), vec.end()) + 1) {}
    
    WaveletMatrix(const vector<T>& vec, const T sigma) {
        vector<T> cp = vec;
        init(cp, sigma);
    }
    void init(vector<T>& vec, const T sigma) {
        if(sigma == 1)
            height = 1;
        else
            height = 64 - __builtin_clzll((unsigned long long)(sigma - 1));
        
        B.resize(height);
        pos.resize(height);
        for (unsigned int i = 0; i < height; ++i) {
            B[i].resize(vec.size());
            for (unsigned int j = 0; j < vec.size(); ++j) {
                B[i].set(j, get(vec[j], height - i - 1));
            }
            B[i].build();
            auto it = stable_partition(vec.begin(), vec.end(), [&](T c){
                return !get(c, height - i - 1);
            });
            pos[i] = it - vec.begin();
        }
    }
    
    // 返回数值 val 在第 i 位的二进制值（0 或 1）
    int get(const T val, const int i) const {
        return int((val >> i) & 1);
    }
    // 查询区间 [l, r) 中数值 val 的频次
    int rank(const T val, const int l, const int r) {
        return rank(val, r) - rank(val, l);
    }
    // 查询 [0, i) 中数值 val 的频次
    int rank(T val, int i) {
        int p = 0;
        for (unsigned int j = 0; j < height; ++j) {
            if(get(val, height - j - 1)) {
                p = pos[j] + B[j].rank1(p);
                i = pos[j] + B[j].rank1(i);
            } else {
                p = B[j].rank0(p);
                i = B[j].rank0(i);
            }
        }
        return i - p;
    }
    
    // 查询区间 [l, r) 中第 k 小的数（k 从 0 开始）
    T quantile(int k, int l, int r) {
        T res = 0;
        for (unsigned int i = 0; i < height; ++i) {
            int zeros = B[i].rank0(l, r);
            if(zeros > k) {
                l = B[i].rank0(l);
                r = B[i].rank0(r);
            } else {
                l = pos[i] + B[i].rank1(l);
                r = pos[i] + B[i].rank1(r);
                k -= zeros;
                res |= (T(1) << (height - i - 1));
            }
        }
        return res;
    }
    T rangemin(const int i, const int j, const T a, const T b,
               const T l, const T r, const int x, const T val) {
        if(i == j || r <= a || b <= l) return -1;
        if(r - l == 1) return val;
        const T mid = (l + r) >> 1;
        T res = rangemin(B[x].rank0(i), B[x].rank0(j), a, b, l, mid, x + 1, val);
        if(res < 0)
            return rangemin(pos[x] + B[x].rank1(i), pos[x] + B[x].rank1(j),
                           a, b, mid, r, x + 1, val + (T(1) << (height - x - 1)));
        else
            return res;
    }
    //查询区间 [l, r) 内，值域 [a, b) 内存在的最小值；若不存在返回 -1
    T rangemin(const int l, const int r, const T a, const T b) {
        return rangemin(l, r, a, b, 0, (T(1) << height), 0, 0);
    }
    T rangemax(const int i, const int j, const T a, const T b,
               const T l, const T r, const int x, const T val) {
        if(i == j || r <= a || b <= l) return -1;
        if(r - l == 1) return val;
        const T mid = (l + r) >> 1;
        T res = rangemax(pos[x] + B[x].rank1(i), pos[x] + B[x].rank1(j),
                          a, b, mid, r, x + 1, val + (T(1) << (height - x - 1)));
        if(res < 0)
            return rangemax(B[x].rank0(i), B[x].rank0(j),
                           a, b, l, mid, x + 1, val);
        else
            return res;
    }
    //查询区间 [l, r) 内，值域 [a, b) 内存在的最大值；若不存在返回 -1
    T rangemax(const int l, const int r, const T a, const T b) {
        return rangemax(l, r, a, b, 0, (T(1) << height), 0, 0);
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

   ### DSU(并查集）

```
class DSU {
public:
    std::vector<int> parent, siz;
    std::unordered_map<int, std::vector<int>> groups;
    std::unordered_set<int> Root;

    DSU(int n) {
        parent.resize(n + 1);
        siz.resize(n + 1, 1);
        std::iota(parent.begin(), parent.end(), 0);
    }

    int find(int x) {
        return parent[x] == x ? x : parent[x] = find(parent[x]);
    }

    bool merge(int x, int y) {
        int Fx = find(x);
        int Fy = find(y);
        if (Fx != Fy) {
            if (siz[Fx] < siz[Fy]) {
                std::swap(Fx, Fy);
            }
            parent[Fy] = Fx;
            siz[Fx] += siz[Fy];
            return true;
        }
        return false;
    }
    bool same(int x, int y) {
        return find(x) == find(y);
    }

    void connect(int n) {
        groups.clear(); // 清空之前的分组结果
        for (int i = 1; i <= n; i++) {
            int root = find(i);
            groups[root].push_back(i);
            Root.insert(root);
        }
    }
};
```

### 单调队列

单调队列在维护单调性的过程中，能够高效地完成队列首元素的删除操作，类似于滑动窗口移动左指针。可用于优化$DP$ 

$O(n)$ 处理定长区间$RMQ$ 问题 ，最经典的莫过于滑动窗口最大值；

```c++
deque<int> inc,dec;
for(int i = 0; i < n; i++) {

        while(!inc.empty() && a[i] <= a[inc.back()]) {//严格单调递增 =
            inc.pop_back();
        }
        inc.push_back(i);
        if(i >= m && inc.front() == i-m) inc.pop_front();
     
        while(!dec.empty() && a[i] >= a[dec.back()]) {//严格单调递减 =
            dec.pop_back();
        }
        dec.push_back(i);
        if(i >= m && dec.front() == i-m) dec.pop_front();
}
```

### LCA

```c++
class TreeLCA {
public:
    int n;
    vector< vector<int> > G;
    vector<int> dep,fa,siz,son,top;
    int maxsize;
    TreeLCA (int n) : n(n) {
        G.resize(n+1);
        dep.resize(n+1,0);
        fa.resize(n+1,0);
        siz.resize(n+1,0);
        son.resize(n+1,0);
        top.resize(n+1,0);
        maxsize = -1;
    }
    void addEdge(int u,int v) {
        G[u].push_back(v);
        G[v].push_back(u);
    }
    void dfs1(int u) {
        siz[u] = 1;
        dep[u] = dep[fa[u]] + 1;
        maxsize = -1;
        for (auto v : G[u]) {
            if(v == fa[u]) continue;
            fa[v] = u;
            dfs1(v);
            siz[u] += siz[v];
            if(siz[v] > maxsize) {
                maxsize = siz[v];  
                son[u] = v;
            }
        }
    }
    void dfs2(int u,int t) {
        top[u] = t;
        if(son[u]) dfs2(son[u],t);
        for (auto v : G[u]) {
            if(v == fa[u] || v == son[u]) continue;
            dfs2(v,v);
        }
    }
    void process(int root = 1) {
        dfs1(root);
        dfs2(root,root);
    }
    int LCA(int u,int v) {
        while(top[u] != top[v]) {
            if(dep[top[u]] >= dep[top[v]])  u = fa[top[u]];
            else v = fa[top[v]];
        }
        return dep[u] < dep[v] ? u : v;
    }
    int dist(int u,int v) {
        return dep[u] + dep[v] - 2 * dep[LCA(u,v)];
    }
};
```
