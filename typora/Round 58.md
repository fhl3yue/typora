### A

签到

```c++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N = 2e6 + 4;


void solve() {
	double a,b;
	std::cin >> a >> b;
	if(a >= b) std::cout << "NO" << '\n';
	else std::cout << "YES" << '\n';
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

### B

签到  只有数位递减才不能

```c++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N = 2e6 + 4;


void solve() {
	std::string s;
	std::cin >> s;
	bool ok = true;
	std::reverse(s.begin(),s.end());
	for(int i = 0; i < s.length() - 1; i++) {
		if(s[i] > s[i+1]) ok = false;
	}
	if(ok == false) std::cout << "YES" << '\n';
	else std::cout << "NO" << '\n';
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

### C

打表 发现

```c++
     #include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
using namespace std;
const int N = 2e3 + 4;
char c[N][N];
void solve() {
	int q;
	std::cin >> q;
	
	while(q--) {
		int x,y;
		std::cin >> x >> y; 
		if(x < 0 || y < 0) std::cout << "PING" << '\n';
		else {
			if(x == y) std::cout << "NO" << '\n';
            else if(x == y - 1 || x == y + 1) std::cout << "YES" << '\n';
            else std::cout << "PING" << '\n';
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

###  D

拆成 $k$进制数 

每个$k$好数只能由每个$k$幂次出现一次  问题转化为最多的$k$幂次个数

从大到小拆分会拆的少一点

最后 为什么爆范围显示 $TLE$呢

要用 __int128

```c++
#include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
const int N = 2e6 + 4;
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

void solve() {
	ull n,k;
	std::cin >> n >> k;
	if(k == 1 || n == k) {
		std::cout << 1 << '\n';
		return;
	}
	if(n < k) {
		std::cout << n << '\n';
		return;
	}
	i128 p = 1,l = 1;  ull ans = 1;
	std::vector<i128> v;
    ull mp[66] = {};
	for(int i = 0; i < 63; i++) {
		v.push_back(p);
		if(p > n) break;
		p = p * k * l;
	}
	while(n > 0) {
		int pos = std::upper_bound(v.begin(),v.end(),n) - v.begin();
		pos--;
        mp[pos] = n / v[pos];
        n -= mp[pos] * v[pos];
        ans = std::max(ans,mp[pos]);
	}
	std::cout << ans << '\n';
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

### E

 发现 $a_i = a_{i+1} mod \quad i$  包含的值域限制

打表

```c++
	// n = 1  0 1
	// n = 2  00 01 02
	// n = 3  002 011 013  000
	// n = 4  0022 0111 0114 0000 0003
	// n = 5  00222 01111 01115 00000 00004 00033
    // n = 6  000000  011111 002222 000333 000044 000005 011116 
```

```c++
#include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
using namespace std;
const int N = 2e3 + 4;

void solve() {
	int n,m; // ai = ai+1 % i
	std::cin >> n >> m;
	if(m > 3) {
		std::cout << 0 << '\n';
		return;
	}
	if(m == 3) {
		std::cout << 1 << '\n';
	}
	if(m == 2) {
		std::cout << n << '\n';
	}
	if(m == 1) {
		// n = 1  0 1
		// n = 2  00 01 02
		// n = 3  002 011 013  000
		// n = 4  0022 0111 0114 0000 0003
		// n = 5  00222 01111 01115 00000 00004 00033
        // n = 6  000000  011111 002222 000333 000044 000005 011116 
		std::cout <<  n + 1 << '\n';
	}
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

### F

关键还是要知道 查询区间第$k$小的数据结构 

可持久化线段树或 小波树

能缩小 $[1,n]$ 幸运数的范围

```c++
#include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
using namespace std;
const int N = 2e3 + 4;
const ll mod = 1e9 + 7;
ll ksm(ll a,ll b) {
	ll res = 1;
	while(b) {
		if(b & 1) res = res * a % mod;
		a = a * a % mod;
		 b >>=1;
	}
	return res;
}
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
    // [l, r) 中k小
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


void solve() {
	int n,m;
	std::cin >> n >> m;
	std::vector<int> a(n+1);
	for(int i = 1; i <= n; i++) std::cin >> a[i];
	WaveletMatrix T(a);
	int L = 1, R = n; // 幸运数范围 不是区间范围
	while(m--) {
		int l,r,k;
		std::cin >> l >> r >> k;
		r++;
		if(k == 0) {
               // 幸运数 小于 区间最小  k = 0，是 意思中的第一小
			R = std::min(T.quantile(k,l,r) - 1 , R);
               //std::cout << T.quantile(k,l,r) - 1 << '\n';
		} else if(k == r - l) {
               // 整个区间都小于等于幸运数  k = 3, 找区间第三小 封装第二小位置
			L = std::max(T.quantile(k-1,l,r) , L);
               //std::cout << T.quantile(k-1,l,r) << '\n';
		} else {
			R = std::min(T.quantile(k,l,r) - 1 , R);
               //std::cout << T.quantile(k,l,r) - 1 << " ";
			L = std::max(T.quantile(k-1,l,r) , L);
               //std::cout << T.quantile(k-1,l,r) << '\n';
		}
	}
	std::cout << ksm(R - L + 1, mod - 2);
	if(R - L + 1 == 1) std::cout << " " << R;
	std::cout << '\n';
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

