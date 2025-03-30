**牛客周赛 Round 38**

**A** :  签到题

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
int n;
int main() {
    cin >> n;
    cout << (10 - (n % 10)) % 10;
    return 0;
}
```

**B** ：  需要一个知识点： 若 一个数是 9  的 倍数 ，则  各数位数之和 也是 9 的 倍数

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 40;
typedef long long ll;
string s;
ll sum,ans;
int main() {
    cin >> s;
    int len = s.length();
    for(int i = 0; i < len ; i++) {
        sum += (s[i] - '0');
        if(sum % 9 == 0) ans++;
    }
    cout << ans ;
    return 0;
}
```

**C** ： 构造一个长为$n$ ,均为小写字母，恰好有$k$ 个 回文子串 的 字符串   

$1 \le n \le 10^{5}$

$0 \le k \le \frac{n}{2}$

被样例骗里，以为只用 OO类字符串不够，开始计算长度 x 的 "OOOOOO" 的贡献 其实没有必要 

最后一串shit代码 108.33 / 125 pts

其实只要 枚举 k 个 两个长度的  ，余下的 用一个长度的 填充即可 

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
typedef long long ll;
int n,k,pos;
int main() {
    cin >> n >> k;
    string s = "";
    string a = "abc", b = "def";
    for(int i = 0,j = 0; i < k; i++) {
        s += a[j];
        s += a[j];
        j = (j + 1) % 3;
    }
    int j = 0;
    while(s.size() < n) {
        s += b[j];
        j = (j + 1) % 3;
    }
    cout << s;
    return 0; 
}
```

**D** ：每次操作在相邻数组间插入一个数 ，平滑值： 相邻两数差值的绝对值的最大值   

让 平滑值 为 K  最少需要 操作几次 

142.50 / 150  

错误原因 ； 忽略了当 差值远小于 K 时 当且仅当需要一次操作 使得平滑值 为 K 

我代码默认了 小于K时  操作次数不添加  

举例 ： 1 3 5 7         12

1/ 13 /3/ 5/ 7/   即可 

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
typedef long long ll;
ll a[N],c[N];
ll n,k,ans;
int main() {
    cin >> n;
    cin >> k;
    for(ll i = 1; i <= n; i++) {
        cin >> a[i];
        c[i] = abs(a[i] - a[i-1]);
    }
    c[1] = 0;
    bool flag  = false;
    for(ll i = 1; i <= n; i++) {
        //cout << c[i] << " ";
        if(c[i] >= k) flag = true;
        ll x = c[i] % k;
        ans += c[i] / k;
        if(c[i] != 0 && x == 0) ans--;
    }
    if(flag == false) ans++;
    cout << ans;
    return 0;
}
```

 **E** : 长度 为 $n$ 的数组 $a$ , 选择最多的 数 使得能够 构成 等比数列 ，公比 $q$ 为 正整数   输出 最多的数量

```txt
5
3 4 2 1 4

3
```

最初的设想是 先排序  利用dp  ，状态量 是 $a[i]$ 作为 等比某一项的  最大 长度   

但是我 dp 很烂 ，不好写 

真的没有想到 能够 枚举 公比  $q$ 

听讲解 ： 公比 q 多× 几次 就能超 数据范围 就算 q = 2 ,也仅需 17 次 完全是 常数级的复杂度 

注意 q = 1 的 情况；

利用 map 标记 数出现次数  每个 a[i] 枚举 × q  看看 是够存在   但是 必须连续  

还有一处 特别巧妙的地方 ：：：

 **pow(q,ans) <= 2e5**    

很多时候 我们 利用 q = 1 或 2 得 到了一个 ans  ，已经比较大了 （假设是10），而且已知 。。

这时我们枚举 公比 10 ，$10^{ans} > 2e5$   那我们根本不用 看10了 ，就算 10为公比 的数在数组中很多  ，但绝对不会多于 $ans$

对我们要进行的 ans 更新没有任何作用 ，大大降低了时间复杂度   

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
typedef long long ll;
const int M = 2007;
int n;
int a[N];
map<int,int> mp;
void solve() {
	cin >> n;
	int ans = 0;
	for(int i = 1; i <= n; i++) {
		cin >> a[i];
		mp[a[i]]++;
		ans = max(ans,mp[a[i]]);
	}
	for(int q = 2; pow(q,ans) <= 2e5 ; q ++) {
		for(int i = 1; i <= n; i++) {
			int now = a[i],cnt = 0;
			while(now <= 2e5 && mp[now] > 0) {
				cnt++;
				now *= q; 
			}
			ans = max(ans,cnt);
		}
	}
	cout << ans << endl;
}
int main() {
	int _ = 1;
	// cin >> _ ;
	while(_ --) {
		solve();
	}
	return 0;
}
```

**更新：数据有加强  现在这个方法只能过 96.88%**  

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e5 + 50;
typedef long long ll;
const int M = 2007;
int n;
void solve() {
	cin >> n;
	int ans = 0;
	vector<int> a(N + 1),cnt(N + 1);
	for(int i = 1; i <= n; i++) {
		cin >> a[i];
		cnt[a[i]]++;
	}
	for(int i = 1; i <= 2e5; i++) {
		ans = max(ans,cnt[i]);
		if(cnt[i] == 0) continue;
		for(int j = i + i; j <= 2e5; j += i) {
			if(cnt[j] == 0) continue;
			int c = 2;
			int now = j;
			int q = j / i;
			while(now <= 2e5 && cnt[now] > 0) {
				ans = max(ans,c);
				now *= q;
				c ++;
			}
		}
	}
	cout << ans << endl; 
}
int main() {
	int _ = 1;
	// cin >> _ ;
	while(_ --) {
		solve();
	}
	return 0;
}
```

**新更改的代码时间复杂度还是不会算 ，主要区别在于枚举 q 改为 枚举 a[i] 的 倍数  ，如果有倍数 就可以算出 q  根据连续的原则 等比地去找**

**F: ** 进行$q$ 次询问，每次问一个区间  $[l,r]$  是否存在 回文子串 （长度 严格大于 2）  （注意子序列 可以不连续 ） 

当时看到题目时就想到 线段树，莫队 树状数组  ，来找 区间有没有 回文串  ，但是没有做过类似的题目 ，不知道 怎么写 就放弃了 

**讲解注意：** 1 1 2 1      发现 一个区间 只要存在有 不相邻的 两个数相等 就一定能满足条件

 **la[i]**   保存的是  $a[i]$  上次出现的坐标 ，其中 $la[i] != i - 1$   

只要区间内有  $la[i]$  且 值 在$[l,r]$ 内 即可   区间 $la[l,r]$ 最大值 $\ge l$  即可  

问题回到区间查询最大值  。。  这样 线段树 , RMQ   可以做了  

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e5 + 50;
typedef long long ll;
const int M = 2007;
int n,q;
int f[M][30];
void solve() {
	cin >> n >> q;
	vector<int> Log(N),a(N),la(N);
	map<int,int> mp;
	for(int i = 1; i <= n; i++) {
		cin >> a[i];
		if(mp.count(a[i])) {
			la[i] = mp[a[i]];
		}
		mp[a[i]] = i;
	}
	for(int i = n; i ; i--) {
		if(la[i] == i - 1) 
		la[i] = la[la[i]];
	}
	//for(int i = 1; i <= n; i++) {
	//	cout << la[i] << " ";
	//}   cout << endl;
	for(int i = 1; i <= n; i++) f[i][0] = la[i];
	Log[1] = 0, Log[2] = 1;
	for(int i = 3; i <= n; i++) Log[i] = Log[i/2] + 1;
	for(int j = 1; j <= Log[n]; j ++) {
		for(int i = 1; i + (1 << j) - 1 <= n; i++) {
			f[i][j] = max(f[i][j-1],f[i + (1 <<(j-1))][j-1]);
		}
	}
	for(int i = 1; i <= q; i++) {
		int l,r;
		cin >> l >> r;
		int p = Log[r - l + 1];
		int pos = max(f[l][p],f[r - (1 << p) + 1][p]);
		if(pos >= l) cout << "YES" << endl;
		else cout << "NO" << endl;
	}
}
int main() {
	int _ = 1;
	// cin >> _ ;
	while(_ --) {
		solve();
	}
	return 0;
}
```

### 这里用的是 **RMQ ST 倍增 求解 区间最大值**

## 什么是RMQ问题

$rmq$ 问题指的是 $range~~maximum/minimum~~query$ （区间最大/最小值询问），给定一个区间左端点 $l$ 和右端点  $r$ ,询问 $[l,r]$ 中最值，一般朴素的做法是利用for循环在 $[l,r]$ 中不断判断更新答案，但这样做的时间复杂度是 $O(n)$ ，再乘上查询次数后时间复杂度更是非常高，这对我们来说非常不理想，因此有三种快速解决RMQ问题的算法

下面以求区间最大值，一共有 $n$ 个数据， $k$ 次询问为例。

## ST表(动态规划+倍增思想）

**算法原理：**

  由于 $rmq$ 问题一个**可重复贡献问题**，而倍增能够快速的覆盖所有元素，所以能够快速地求解出任意区间的最大值，ST表本身是一个数据结构，一般用二维数组来存储。

**实现过程**（**下标从 $1$ 开始**）：

$(1)$ 令 $f[i][j]$ 的含义为以 $i$ 为起始点（左端点），区间长度为 $2^j$ 的最大值。区间表示就是 $[i,i+2^j-1]$ ，如果将区间一分为而，则得到 $[i,i+2^{j-1}-1]$ 和 $[i+2^{j-1},i+2^j-1]$ ，这两个子区间的各自的最大值再取一次最大值就是大区间的最大值

$(2)$ 由 $(1)$ 明白了某个区间可以划分中点，这个区间最大值可以由左右区间得来，那我们用状态转移方程的语言去表达就是 $[i,i+2^{j-1}-1]\longrightarrow f[i][j-1]$ 及 $[i+2^{j-1},i+2^j-1]\longrightarrow f[i+2^{j-1}][j-1]$ 整理就可以得到 $f[i][j]=min(f[i][j-1],f[i+2^{j-1}][j-1])$ 

$(3)$ 对于初始化：我们根据定义 $f[i][0]$ 代表以下标 $i$ 开头并有 $2^0=1$ 个元素的区间最大值，此时不难发现这个区间只有 $a[i]$ 自身，那么最值肯定也是其本身，所以 $f[i][0]=a[i]$ ，另外，我们发现 $j$ 是 $2$ 的幂， $j$ 的取值不应该太大，其极限取值应该是 $log_2n$ ，以及我们后续查询也需要将区间长度取对数，为了快速得到 $log_2x$ 的值，需要对数表数组 $log[i]$ ，初始化为 $log[1]=0,log[2]=1$ ，往后递推 $log[i]=log[i/2]+1$ 。

$(4)$ 循环范围：发现 $j$ 由 $j-1$ 得来，所以可以外层循环 $j$ 从 $[1,log[n]]$ （ $0$ 的情况已经在初始化得出），内层循环 $i$ 从 $[1,n]$ ，但右端点(即区间结束点)的取值不可以超过 $n$ ，由 $(1)$ 得到 $i+2^j-1<=n$ 

$(5)$ 查询：对于一个区间 $[a,b]$ ，其长度对数 $p=log[b-a+1]$ ，我们可以划分成两个区间（注意这里不能再从中间一分为二了，因为长度不一定是 $2$ 的幂，奇数长度有可能会决策到额外的数），从左开始为 $[a,a+2^p]$ ，从右开始为 $[b-2^p+1,b]$ ，这分别代表了「从 $a$ 开始的 $2^p$ 个数」、「从 $b$ 结尾的 $2^p$ 个数」。这两个区间一定能够覆盖 $[a,b]$ （这里不作证明），故查询结果应该是 $max(f[a][p],f[b-2^p][p])$ 

**最终代码：**

注意在刚刚的描述中 $2^j$ 只是为了方便描述，实际编码应该用 $1<<j$ 来写入

**G:** 给定 长度为$n$  的 数组 $a$  ，从 $a$ 中 删除 一个区间 ，使得剩余拼接起来的区间的 逆序对数量 不少于 $k$  ,  求删除区间  方案数 

 常见的求 逆序对有两种方法，归并排序和树状数组。  这道题是明显的有修改趋势，要通过树状数组来求逆序对 。

3 1  2 5                1 2 3 5  

树状数组求逆序对的原理是：  类似桶排序 放的位置， 将放的数    看已经有多少 比它大的数已经放过了 ，或者倒着放，看有多少值比它小   。。。 针对值域较小的情况，值域较大的话，需要用到离散化。。。  

我们来看 少了一个数 ，逆序对发生了什么变化：   逆序对减少了  左边比它大的，右边比它小的  

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
typedef long long ll;
const int M = 2007;	
ll n,m,k,cnt;
ll a[N];
vector<ll> tr1(1000001),tr2(1000001);
ll lowbit(ll i) {
	return i & (-i);
}
void add(vector<ll> & tr,ll x,ll k) {
	for(ll i = x; i <= 1e6; i += lowbit(i)) {
		tr[i] += k;
	}
}
ll getsum(vector<ll> & tr,ll x) {
	ll res = 0;
	for(ll i = x; i ; i -= lowbit(i)) {
		res += tr[i];
	}
	return res;
}
void solve() {
	cin >> n >> m; 
	ll sum = 0;
	//vector<int> a(n + 1);
	for(ll i = 1; i <= n; i++) {
		cin >> a[i];	
	}
	for(ll i = n; i ; i --) {
		add(tr2,a[i],1);
		sum += getsum(tr2,a[i] - 1);
	}
	// 当前 sum  为  给定原序列的逆序对数 
	ll ans = (sum >= m);  
	// 维护 双指针 （滑动窗口）  必需 删除的区间 
	for(ll i = 1, j = 1; i <= n; i ++) {
		add(tr2,a[i],-1);  // 删除 a[i]
		sum -= getsum(tr2,a[i] - 1);// 左侧的 
		sum -= getsum(tr1,1e6) - getsum(tr1,a[i]); // 右侧 
		while(j <= i && sum < m) { // 把 已经删除的a[j] 加上 
			add(tr1,a[j],1);
			sum += getsum(tr2,a[j] - 1);
			sum += getsum(tr1,1e6) - getsum(tr1,a[j]);
			j ++;
		}
		ans += (i - j + 1);
 	}
	cout << ans << endl;
}
int main() {
	int _ = 1;
	//cin >> _ ;
	while(_ --) {
		solve();
	}
	return 0;
}
```





