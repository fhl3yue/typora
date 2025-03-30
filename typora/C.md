**前面**

监狱每次$div2$第三题及以上劳氏做不出来（菜就多练） 和$kk$故意不AK 导致CF劳氏上不去分   故决定 怒刷$CFdiv2$ C 寄 D(if have easy) 

$update: 942$

$C:$

You have some cards. An integer between $1$ and $n$ is written on each card: specifically, for each $i$ from $1$ to $n$, you have $a_i$ cards which have the number $i$ written on them.

There is also a shop which contains unlimited cards of each type. You have $k$ coins, so you can buy $k$ new cards in total, and the cards you buy can contain any integer between $1$ and $n$.

After buying the new cards, you rearrange all your cards in a line. The score of a rearrangement is the number of (contiguous) subarrays of length $n$ which are a permutation of $[1, 2, \ldots, n]$. What's the maximum score you can get?

题意： $1-n$ 每个都有$a_i$  张卡片，上面有数字$i$ ，可以购买$k$ 张新卡片，购买的卡片数字是$1-n$ 任意数，将所有卡片重新排列成一行，重新排列的得分是长度为$n$ 的(连续)子数组中 $[1,2,…,n]$的排列数 ，求最高分。  （$t \le 100,n \le 2 \times 10^5, k \le 10^{12},a_i \le 10 ^{12}$ ），$\sum n  \le 5 \times 10 ^ 5$

跳了跳了 看不懂思密达

$D:$ 

给你两个正整数 $$n$$$ , $$$m$$ 。

计算满足以下条件的有序数对 $$(a, b)$$ 的个数：

- $1\le a\le n$$  1\le b\le m$ ;

- $a+b$$ 是 b \cdot \gcd(a,b)$ 的倍数。

  $\sum _{a = 1} ^ {n}\sum _{b = 1} ^ {m} [(a + b) \equiv 0 (\mod (b \times gcd(a,b)) ]$

  看着能用莫比乌斯函数和整式的变换成能整数分块的形式     但是我没能化出来  没开始写代码就放弃了 

  现在参考题解 ： 

  $d = gcd(a,b)$  ->    $a = p \times d$   $b = q \times d$    

  $gcd(p,q) = 1$  

  $a + b / (b \times gcd(a,b))$ = ($pd + qd$) / ($qd^2$)  = $\frac{p+q}{qd}$ = $k$

  观察 题目给的 样例解释  发现 $b$ 是 $a$ 的因子  --> $q = 1$

  $k = \frac{p+1}{d}$   

  找有多少个 $k$ 是整数 

  枚举$d$  ($1 \le d \le m$)   ($n < m$ 时的 $d$   计算上对答案也没有贡献)

  找有多少个 $p$    根据$p$ 的意义   （$1 \le a \le n$ )  

  $\sum_{d=1}^{m}\sum [\frac{p+1}{d}]$  =  $\sum_{d=1}^{m} \frac{\frac{n}{d} + 1}{d}$   （这一步推导存疑）

   $1 - n$中有多少  % $d$ = 0  的个数    -->   $\left\lfloor\dfrac{n}{d}\right\rfloor$  

  当 d = 1,p = 0,k = 1,时也被计算上。

  ```c++
  #include <bits/stdc++.h>
  using namespace std;
  const int N = 2e6 + 50;
  const int M = 2007;
  const int P = 1e9 + 7;
  const long long INF = 1e18;
  typedef long long ll;
  ll n,m,k;
  void solve() {
      cin >> n >> m;
      ll ans = 0;
      for(ll d = 1; d <= m; d ++) {
          ans += (ll)(n + d) / (ll)(d * d);
      }
      ans -= 1;
      cout << ans << endl;
      return;
  }
  int main() {
      int _ = 1;
      cin >> _;
      while(_ --) {
          solve();
      }
      return 0;
  }
  ```

**edu 165**

**C:**

给你一个长度为 $$n$$的整数数组 $$a$$ 。

您可以执行以下操作：选择数组中的一个元素，并用其邻近元素的值替换它。

例如，如果是 $$a=[3, 1, 2]$$ ，则可以通过一次操作得到数组 $$[3, 3, 2]$$$ 、 $$$[3, 2, 2]$$$ 和 $$$[1, 1, 2]$$ 中的一个，但不能得到 $$[2, 1, 2$$$ ] 或 $$$[3, 4, 2]$$ 。

你的任务是计算数组的最小总和，如果你能执行上述操作最多 $$k$$ 次的话。

自己做了 做错了，发现这不是贪心，贪心的修改后最优解会变化  大概是$dp$

别人的题解视频：

$dp[i][j]$  前$i$个数做$j$次操作的最小和 

到达$i$ ，可以不做操作 $dp[i][j] = dp[i-1][j] + a[i]$

做操作：  

由于 $k \le 10$

可以枚举 前$i$个数做（1 - $k$）次 操作  

将$[i-k,i]$（区间共 $k+1$个数) 每个数变成 $a[i-k-1]$ (前提前面的小)  那么边界也很清楚了

时间复杂度$O(nk^2)$ 

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 1e6 + 50;
const int M = 2007;
const int P = 1e9 + 7;
const long long INF = 1e18;
typedef long long ll;
ll n,m,k;
ll a[N];
ll dp[N][11];
void solve() {
    cin >> n >> m;
    for(int i = 1;i <= n; i++) cin >> a[i];
    for(int i = 1; i <= n; i++) {
        for(int j = 0; j <= m; j++) 
        dp[i][j] = INF;
    }
    for(int i = 1; i <= n; i++) {
        for(int j = 0; j <= m; j++) {
            dp[i][j] = dp[i-1][j] + a[i];
            ll minx = a[i];
            for(int k = 1; (i - k - 1 >= 0) && k <= j; k ++) {
                minx = min(minx,a[i - k]);
                dp[i][j] = min(dp[i][j],dp[i - k - 1][j - k] + minx * (k + 1));
            }
        }
    }
    cout << dp[n][m]<< endl;
}
int main() {
    int _ = 1;
    cin >> _;
    while(_ --) {
        solve();
    }
    return 0;
}
```





**cf  941 **

**C:**  最有希望的一题

爱丽丝和鲍勃正在玩一个关于 $$n$$ 堆石子的游戏。轮到每个棋手时，他们都会选择一个正整数 $$k$$ ，这个正整数最多等于最小的非堆的大小，然后从每个非空堆中一次性取出 $$k$$ 个石子。第一个无法下棋的棋手(因为所有棋子都是空的)输。

既然爱丽丝先下，那么如果双方都以最佳方式下棋，谁会赢呢？

因为每次对所有堆都修改  我们想到了差分

排序差分后我们发现 谁先第一个取（大于差分结果2 ）的一堆  ，就能通过操作  使得每一次都能第一个取大于2或者最后一个

就是这么简单的规律  却写挂了  

天要亡我？！

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
const int M = 2007;
const int P = 1e9 + 7;
const long long INF = 1e18;
typedef long long ll;
int n,m,k;
ll a[N];
ll b[N]; // 差分数组  
char c[M][M];
void solve() {
    cin >> n;
    for(int i = 1; i <= n; i++) {
        cin >> a[i];
    }
    sort(a + 1,a + n + 1);
    for(int i = 1; i <= n; i++) {
        b[i] = a[i] - a[i - 1];
    }
    bool flag = false;
    int cnt = 0;
    for(int i = 1; i <= n; i++) {
        if(b[i] >= 1) flag = 1 - flag;
        if(b[i] > 1)  break;
    }
    if(flag == false) cout << "Bob" << endl;
    else cout << "Alice" << endl;
    return;
}
int main() {
    int _ = 1;
    cin >> _;
    while(_ --) {
        solve();
    }
    return 0;
}
```

 **ABC 352**

D:读懂题目很重要 

求 $k$个 数相差为1 的最短区间长度 

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 1e6 + 50;
const int M = 2007;
const int P = 1e9 + 7;
const long long INF = 1e18;
typedef long long ll;
int n,m,k;
void solve() {
    cin >> n >> k;
    vector<int> p(n + 1);
    for(int i = 0; i < n; i++) {
        int x;
        cin >> x;
        x--;
        p[x] = i;
    }
    int ans = n;
    set<int> s;
    for(int i = 0; i < n; i++) {
        s.insert(p[i]);
        if(i >= k) {
            s.erase(p[i - k]);
        } 
        if(i >= k - 1) {
            ans = min(ans, *s.rbegin() - *s.begin());
        }
    }
    cout << ans << '\n';
    return ;
}
int main() {
    int _ = 1;
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);  
    //cin >> _;
    while(_ --) {
        solve();
    }
    return 0;
}
```



E:

求图的最小生成树  

关键的一点是  按照题意建边需要再开一个循环，时间复杂度 $O(n^2)$   ,  需要建立数个虚点 ，让它们连向对应节点 。

对整个大图做 $Kruskal$ 会导致最后的结果多算了，  观察图中多余被算上的部分，  减去。 

```c++
#include <bits/stdc++.h>
using namespace std;
const int N =  2e6 + 82;
struct node{
    int u;
    int v;
    int w;
}t[N];
int fa[N];
bool cmp(node a,node b) { return a.w < b.w ; }
int find(int x) {
    return fa[x] == x ? x : fa[x] = find(fa[x]);
}
using i64 = long long;
int n,m;
int main() {
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0); 
    i64 ans = 0;
    cin >> n >> m;
    for(int i = 1; i <= n + m; i++) {
        fa[i] = i;
    }
    int cnt = 0,pot = n + m,num = 0;
    for(int i = 1; i <= m; i++) {
        int x,y;
        cin >> x >> y;
        for(int k = 1; k <= x; k ++) {
            int p; 
            cin >> p;
            t[++cnt] = {i + n,p,y};
        }
        ans -= y;
    }// cnt 边 pot 点
    sort(t + 1,t + cnt + 1,cmp);
    for(int i = 1; i <= cnt; i++) {
        int u = t[i].u,v = t[i].v,w = t[i].w;
        int fau = find(u),fav = find(v);
        if(fau != fav) {
            fa[fau] = fav;
            ans += w;
            num++;
            if(num == pot - 1) break;
        }
    }
    if(num != pot - 1) cout << -1 << endl;
    else  cout << ans <<  endl;
    return 0;
}
```

**XOUR  **

给你一个由 $n$ 个非负整数组成的数组 $a$ 。

如果 $a_{i} XOR a_j \quad < 4$ ，你可以交换位置 $i$ 和 $j$ 的元素，其中 $\mathsf{XOR}$ 是 [bitwise XOR 运算](https://en.wikipedia.org/wiki/Bitwise_operation#XOR)。

求任意交换次数所能组成的最小数组的序数。

如果在 $x$ 和 $y$ 不同的第一个位置，$x_i < y _i$，那么数组 $x$ 在词法上比数组 $y$ 小。



**101101 XOR   101110**  如果两个数$XOR$ 值 小于 4 那么 数的二进制数的最后两位可以不同 但是前面的必须相同 

将前面相等的数 看成一个集合  集合里面的数可以随意交换 显然排序即满足要求  

通过 $priority\_ queue$ 来 排序  默认从大到小

也可以 $priority\_queue<int, vector<int>, greater<int> > q;$  设置成小的优先级更高。  

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 2e6 + 50;

void solve()
{
    int n;
    cin >> n; 
    vector<int> a(n + 1);
    map<int, priority_queue<int> > mp;
    for(int i = 0; i < n; i++) {
        cin >> a[i];
        mp[a[i] >> 2].push(-a[i]);
    }
    for(int i = 0; i < n; i++) {
        cout << -mp[a[i] >> 2].top() << " ";
        mp[a[i] >> 2].pop();
    }
    cout << "\n";
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    int _ = 1;
    cin >> _ ;
    while(_ --)
    {
        solve();
    }
    return 0;
}

```

  **C. Ticket Hoarding**

贪心   

发现 只要按照 价格低的票多买就行  

因为后面加的只是前面买过的票的数量  

排序  这样明确 价格低的票 

```c++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 2e6 +50;

void solve()
{
    int n,m,k;
    cin >> n >> m >> k;
    vector<int> a(n);
    for(int i = 0; i < n ; i ++) {
        cin >> a[i];
    }
    sort(a.begin(),a.end());
    ll ans = 0,num = 0,pos = 0;
    for(int i = 0; i < n; i++) {
        num = min(k,m);
        ans += (num * ( a[i] + pos ) );
        pos += num;
        k -= num;
    }
    cout << ans << '\n';
    return;
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);cout.tie(0);
    int _ = 1;
    cin >> _ ;
    while(_ --)
    {
        solve();
    }
    return 0;
}

```

****

