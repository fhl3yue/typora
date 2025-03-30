**牛客周赛 Round 45**

**A**   签到题

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
#define popcount(x) __builtin_popcount(x)

void solve()
{
    int a,b,c,d,e;
    std::cin >> a >> b >> c >> d >> e;
    std::cout << (( (a + b + c + d + e) > 100 ) ? "YES" : "NO") << '\n';
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

**B**

需要转两个弯的签到题

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
#define popcount(x) __builtin_popcount(x)

void solve()
{
    int n,m;
    std::cin >> n >> m;
    if(m == 1) { std::cout << "YES"; return; }
    if(n % 2 == 0) {
        std::cout <<"YES";
        return;
    }
    else if(m & 1) {
        std::cout <<"YES";
        return;
    }
    std::cout << "NO";
    return;
}
// 3 * 3 
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



**C** 题目很容易理解  枚举 递归 记忆化 

```c++
    #include <bits/stdc++.h>
    typedef long long ll;
    const int N = 2e6 + 50;
    #define popcount(x) __builtin_popcount(x)
    int f[N];

    bool check(int x) {
        if(f[x] == 1) return true;
        if(f[x] == -1) return false;
        int p = x,cur = 0;
        while(p > 0) {
            cur += p % 10;
            p /= 10;
        }
        if(cur & 1) {
            f[x] = -1;
            return false;
        }
        if(cur == x)  {
            f[x] = 1;
            return true;
        } 
        if(cur < x && check(cur) == true) {
            f[x] = 1;
            return true;
        }
        return false;
    }
    void solve()
    {
        int n,m;
        std::cin >> n;
        int ans = 0;
        for(int i = 1; i <= n; i++) {
            if(check(i))  ans++;
        }
        std::cout << ans << '\n';
        return;
    }
    // 3 * 3 
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

**D**  思维题 算是 $two point$    核心代码很短但却越容易写错 

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 2e6 + 50;
#define popcount(x) __builtin_popcount(x)
int pos[N];
void solve()
{
    int n,k;
    std::cin >> n >> k;
    std::vector<int> a(n+1);
    for(int i = 1; i <= n; i++) {
        std::cin >> a[i];
    }
    int j = 0;
    ll ans = 0;
    for(int i = 1; i <= n; i++) {
        if(pos[a[i]]  && i - pos[a[i]] > k) {
            j = std::max(j,pos[a[i]]);
        }
        ans += i - j;
        pos[a[i]] = i;
    }
    std::cout << ans << "\n";
    return;
}
// 3 * 3 
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

注意更换$j$ 的位置时 不要用上一次出现的位置简单替换  一定注意 j 是递增的  

最关键一行  十八行 

**E**  算是思维题  

简单描述一下题意  

树   问有多少个点到其余所有点的距离都小于等于 2 



一个点  开始     所有与它直接相连的点(u)  + 1       

所有与u 直接相连的点  加上      

看看sum 是否为 n - 1   

不会有多算的   因为树上无环  



```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 3e5 + 50;
#define popcount(x) __builtin_popcount(x)

void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> v[N];
    for(int i = 1,x,y; i < n; i++) {
        std::cin >> x >> y;
        v[x].push_back(y);
        v[y].push_back(x);
    }
    ll ans = 0;
    for(int i = 1; i <= n; i++) {
        ll sum = 0;
        for(auto u : v[i]) {
            sum += 1;
            sum += v[u].size() - 1;
        }
        if(sum == n - 1) ans++;
    }
    std::cout << ans << '\n';
    return;
}
// 3 * 3 
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

 可笑的是我还分析性质      什么深度大于5一定没有解了   

满足性质的答案一定在  某一层或者某两层   然后枚举这两层    出题人会不知道重点构图这两层吗  唉

**F**  

纯粹的补体力

小橙拥有了一张随机生成的竞赛图，他喜欢图上的三元环，即由三个点组成环，请你帮她求出图上有多少个三元环。

 竞赛图是一个有向图，任意不同的两点间都恰好有一条单向边。也就是一共有$n * (n - 1) / 2$ 条有向边。

伪代码

```python

def rnd():
    ret = seed
    seed = (seed * 7 + 13) mod 1000000007
    return ret mod 2

for i = 1 to n - 1:
    for j = i + 1 to n:
        if rnd() == 0:
            add_edge(i, j) # 从i到j添加一条有向边
        else:
            add_edge(j, i) # 从j到i添加一条有向边
```

思维题 

一个符合要求的三元环  其中每个点都符合出度 = 入度 = 1 

一个竞赛图有多少个三元环：  $n * (n-1) * (n-2) / 6$    $C_n^3$  个  

什么条件不符合要求 

从一个点$i$ 引出两条边      这样三个点一定不符合要求的三元组  $C_{deg[i]}^2$ 数量  

相减就好 

```c++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 3e5 + 50;
const int mod = 1e9 + 7;
#define popcount(x) __builtin_popcount(x)
ll n,seed;
int deg[N];
ll rnd() {
    ll ret = seed;
    seed = (seed * 7 + 13) % mod;
    return ret % 2;
}
void solve()
{
    std::cin >> n >> seed;
    if(n <= 2) {std::cout << 0 <<'\n'; return; }
    for(int i = 1; i < n; i++) {
        for(int j = i + 1; j <= n; j++) {
            if(rnd() == 0)  deg[i]++;
            else deg[j]++;
        }
    }
    ll num = 1ll * (n - 1) * 1ll * (n - 2) * 1ll * n / 6; 
    for(int i = 1; i <= n; i++) {
        num -= 1ll * deg[i] * 1ll * (deg[i] - 1) / 2;
    }
    std::cout << num << "\n";
    return;
}
// 3 * 3 
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

**竞赛图**（tournament graph）是一个有向图，其中每一对顶点之间恰有一条有向边。这意味着对于任意两个不同的顶点 \( u \) 和 \( v \)，要么存在从 \( u \) 指向 \( v \) 的有向边 \( (u, v) \)，要么存在从 \( v \) 指向 \( u \) 的有向边 \( (v, u) \)，但不会同时存在。

竞赛图具有以下一些重要性质：

1. **Hamilton路径与Hamilton回路**:
   - **Hamilton路径**：一个竞赛图总是存在一个Hamilton路径，即经过所有顶点且每个顶点恰经过一次的有向路径。
   - **Hamilton回路**：一个竞赛图存在Hamilton回路的充要条件是图是强连通的（strongly connected）。这意味着图中的任意一对顶点之间存在一条有向路径。

2. **完全竞争图**：
   - 竞赛图的每一对顶点之间都存在唯一的一条有向边，因此一个n阶的竞赛图（即有n个顶点的竞赛图）总共有 \( \frac{n(n-1)}{2} \) 条边。
   
3. **王氏不等式**:
   - 在任意一个n阶竞赛图中，存在一个顶点，其出度至少为 \( \lceil \frac{n-1}{2} \rceil \)。

4. **主顶点（King）**:
   - 在一个n阶竞赛图中，总是存在一个顶点可以通过至多两步到达其他所有顶点。这种顶点称为主顶点（King）。

5. **反馈弧集（Feedback Arc Set）**:
   - 竞赛图中的反馈弧集是一个能够将图中的所有环破坏的最小有向边集。对于竞赛图，可以通过某种排序（即线性排序）来找到一个最小的反馈弧集。

6. **局部性和全局性**:
   - 竞赛图的许多全局性质可以通过局部性质来推导。例如，如果在一个竞赛图的某个子集中存在Hamilton路径，那么在整个竞赛图中也可能存在Hamilton路径。

7. **强连通性**:
   - 如果一个竞赛图是强连通的，则从任意一个顶点出发都可以到达其他任意顶点。这是竞赛图存在Hamilton回路的一个必要条件。

竞赛图在理论计算机科学、组合优化和图论中有着广泛的应用。例如，它们可以用于表示锦标赛的赛程安排、对比较复杂系统的优劣关系建模等。 by chatgpt 

 