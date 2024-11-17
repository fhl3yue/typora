**DP**

  ```mermaid
  graph TD;
  DP-->状态分析
  DP-->状态计算
  状态分析--> 集合
  状态分析--> 属性
  状态计算--> f(i,j)
  ```

**背包问题**

**线性DP**

   	最长严格上升子序列 

​		（N $\le$ $10^6$)   处理方法  

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int n;
vector<int> v;
const int N = 2e6 + 50;
int w[N];
int main()
{
    cin>>n;
    for(int i = 1; i <= n; i++) cin>>w[i];
    v.push_back(w[1]);
    for(int i = 2; i  <= n; i++)
    {
        if(w[i] > v.back()) v.push_back(w[i]);
        else *lower_bound(v.begin(),v.end(),w[i]) = w[i];
    }
    cout<<v.size();
    return 0;
}

/*
3 1 2 1 8 5 6
v:  3

v: 1
v: 1 2
v: 1 2
v: 1 2 8 
v: 1 2 5 
v: 1 2 5 6
*/
```



 **区间DP**

**树形DP**

1.  **树的重心** 

   给定一颗树，树中包含 $n$ 个结点 (编号 $1 \sim n$ ) 和 $n-1$ 条无向边。  
   请你找到树的重心，并输出将重心删除后，剩余各个连通块中点数的最大值。  
   重心定义：重心是指树中的一个结点，如果将这个点删除后，剩余各个连通块中点数的最大值最小，那么这个节点被称为树的重心。  

   **输入格式**  
   第一行包含整数 $n$ ，表示树的结点数。  
   接下来 $n-1$ 行，每行包含两个整数 $a$ 和 $b$ ，表示点 $a$ 和点 $b$ 之间存在一条边。  

   **输出格式**  
   输出一个整数 $m$ ，表示将重心删除后，剩余各个连通块中点数的最大值。  

   **数据范围**  
   $$
   1 \leq n \leq 10^{5}
   $$

![](C:\Users\LWQ\Desktop\Admin\photo\微信图片_20240203202112.png)

对树的遍历可以套用 树链剖分的 dfs1     得出 子树 size

删除 某个点（以 2 举例）   剩余各连通块 由 （2 的 子树 ） （整个树 -  以 2 为根的子树） 组成   

res 取  最大的 连通块 

ans  取 最小的 res 即可 

```c++
#include <iostream>
#include <cstdio>
using namespace std;
const int N = 2e6 + 50;
const int INF = 1e9 + 7;
struct node{
    int from;
    int to;
    int next;
}e[N];
int cnt;
int head[N];
void add(int u,int v)
{
    cnt++;
    e[cnt].from = u;
    e[cnt].to = v;
    e[cnt].next = head[u];
    head[u] = cnt;
}
int ans = INF;
int n;
int father[N],son[N],siz[N],dep[N];
void dfs1(int x)
{
    int res = 0;
    siz[x] = 1;
    dep[x] = dep[ father[x] ] + 1;
    int maxsize = -1;
    for(int i = head[x]; i ; i = e[i].next)
    {
        int y = e[i].to;
        if(y == father[x]) continue;
        father[y] = x;
        dfs1(y);
        res = max(res,siz[y]);
        siz[x] += siz[y];
        if(siz[y] > maxsize) 
        {
            maxsize = siz[y];
            son[x] = y;
        }
    }
    res = max(res,n - siz[x]);
    ans = min(ans,res);
}
int main()
{
    scanf("%d",&n);
    for(int i = 1,a,b; i <= n - 1; i ++)
    {
        scanf("%d%d",&a,&b);
        add(a,b);
        add(b,a);
    }
    dfs1(1);
    printf("%d",ans);
    return 0;
}
```

2. **树的直径 **

   树中两点间的不重复经过的边和点道路称为两点的路径，路径的长度（路径上所经边的长度和）称为两点的距离。圆的直径是一个圆的最长的一条弦，而树的直径是树中两点间最长的路径。通常用一个无序点对 $(x, y)$ 表示一棵树的直径。  

   现在输入一个有 $n$ 个结点的树，结点编号为 1 到 $n$ ，假设结点1为根。试求树的直径。  
   输入格式  
   输入包含 $n+1$ 行，第一行为 1 个正整数 $n$ ，表示树的结点个数。  
   接下来 $n-1$ 行，每行两个整数 $x$ 和 $y$ ，表示结点 $x$ 和 $y$ 之间有一条边，其中 $x$ 是 $y$ 的父亲。  
   输出格式  
   输出只有一个整数，为树的直径。  
   数据范围  
   $$
   \mathrm{n} \leq 10^{5}
   $$

![](C:\Users\LWQ\Desktop\Admin\photo\微信图片_20240203225807.png)

如图 ： 最长直径为 6 + 7 + 9 = 22 

任取一点 u   设置两个变量 d1,d2  

分别统计 以u 点 为 根节点的 最长长度 和 次长长度   d1 + d2  即为 一条直径 

d = dfs(y) + e[i].dis;  // 状态转移  

ans  =  max(ans, d1 + d2);    

```c++
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <cstring>
using namespace std;
typedef long long ll;
const int N = 2e6 + 50;
struct node{
    int from;
    int to;
    int dis;
    int next;
}e[N];
int cnt; int head[N];
void add(int u,int v,int w){
    ++cnt;
    e[cnt].from = u;
    e[cnt].to = v;
    e[cnt].dis = w;
    e[cnt].next = head[u];
    head[u] = cnt;
}
int n,m;
int father[N];
int ans;
int dfs(int x) {
    int d1 = 0;
    int d2 = 0;
    for(int i = head[x]; i ; i = e[i].next){
        int y = e[i].to;
        if(y == father[x]) continue;
        father[y] = x;
        int d = dfs(y) + e[i].dis;
        if(d >= d1) {
            d2 = d1;
            d1 = d;
        }
        else if(d >= d2)  d2 = d;
    }
    ans = max(ans, d1 + d2);
    return d1;
}
int main()
{
    scanf("%d%d",&n,&m);
    for(int i = 1; i <= m; i++){
        int a,b;
        scanf("%d%d",&a,&b);
        add(a,b,1);
        add(b,a,1);
    }
    dfs(1);
    printf("%d",ans);
    return 0;
}

```



3. **换根DP**

给定一个 $n$ 个点的树，请求出一个结点，使得以这个结点为根时，所有结点的深度之和最大。

一个结点的深度之定义为该节点到根的简单路径上边的数量。

第一行有一个整数，表示树的结点个数 $n$。  
        接下来 $(n - 1)$ 行，每行两个整数 $u, v$，表示存在一条连接 $u, v$ 的边。

输出一行一个整数表示你选择的结点编号。如果有多个结点符合要求，输出任意一个即可。

```
8
1 4
5 6
4 5
6 7
6 8
2 4
3 4
```

```
7
```

对于全部的测试点，保证 $1 \leq n \leq 10^6$，$1 \leq u, v \leq n$，给出的是一棵树。

![image-20240205153350232](C:\Users\LWQ\AppData\Roaming\Typora\typora-user-images\image-20240205153350232.png)

假设开始 1 为根  换成 2 为根  

2 的 子树深度 全部加一  

其余树节点 深度全部减一  

f[y] = f[x] - size[y] + n - size[y];  

该转移方程 唯一需要预处理的点是 f[1]  

注意 f[] 开 long long

```
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <cstring>
using namespace std;
typedef long long ll;
const int N = 2e6 + 40;
struct  edge{
    int from;
    int to;
    int next;
}e[N];
int head[N],cnt;
void add(int u,int v)
{
    ++cnt;
    e[cnt].from = u;
    e[cnt].to = v;
    e[cnt].next = head[u];
    head[u] = cnt;
}
int father[N],siz[N],dep[N],son[N];
int f[N];
int ans,pos;
void dfs(int x){
    siz[x] = 1;
    dep[x] = dep[ father[x]] + 1;
    f[1] += dep[x];
    for(int i = head[x]; i ; i = e[i].next){
        int y = e[i].to;
        if(y == father[x]) continue;
        father[y] = x;
        dfs(y);
        siz[x] += siz[y];
    }
} 
int n;
void init(int x) {
    for(int i = head[x]; i ; i = e[i].next){
        int y = e[i].to;
        if(y == father[x]) continue;
        father[y] = x;
        f[y] = f[x] - siz[y] + n - siz[y]; 
        init(y);
    }
}
int main()
{
    cin>>n;
    for(int i = 1,a,b; i <= n - 1; i ++){
        cin>>a>>b;
        add(a,b);
        add(b,a);
    }
    dfs(1);
    init(1);
    for(int i = 1; i <= n; i++) {
        if(ans < f[i]) {
            ans = f[i];
            pos = i;
        }
    }
    cout<<pos;
    return 0;
}

```

4. **换根DP**  [积蓄程度]([287. 积蓄程度 - AcWing题库](https://www.acwing.com/problem/content/289/))  

   有一个树形的水系，由 $N-1$ 条河道和 $N$ 个交叉点组成。  
   我们可以把交叉点看作树中的节点，编号为 $1 \sim N$ ，河道则看作树中的无向边。  
   每条河道都有一个容量，连接 $x$ 与 $y$ 的河道的容量记为 $c(x, y)$ 。  
   河道中单位时间流过的水量不能超过河道的容量。  
   有一个节点是整个水系的发源地，可以源源不断地流出水，我们称之为源点。  
   除了源点之外，树中所有度数为 1 的节点都是入海口，可以吸收无限多的水，我们称之为汇点。  

   也就是说，水系中的水从源点出发，沿着每条河道，最终流向各个汇点。  
   在整个水系稳定时，每条河道中的水都以单位时间固定的水量流向固定的方向。  
   除源点和汇点之外，其余各点不妃存水，也就是流入该点的河道水量之和等于从该点流出的河道水量之和。  

   整个水系的流量就定义为源点单位时间发出的水量。  
   在流量不超过河道容量的前提下，求哪个点作为源点时，整个水系的流量最大，输出这个最大值。

    

   输入格式  
   输入第一行包含整数 $T$ ，表示共有 $T$ 组测试数据。  
   每组测试数据，第一行包含整数 $N$ 。  
   接下来 $N-1$ 行，每行包含三个整数 $x, y, z$ ，表示 $x, y$ 之间存在河道，且河道容量为 $z_{0}$  

   节点编号从 1 开始。  
   输出格式  
   每组数据输出一个结果，每个结果占一行。  
   数据保证结果不超过 $2^{31}-1$ 。  
   数据范围  
   $$
   N \leq 2 \times 10^{5}
   $$

```
1
5
1 2 11
1 4 13
3 4 5
4 5 10

26
```

![](C:\Users\LWQ\Desktop\Admin\photo\微信图片_20240205221511.png)

流量不超过河道流量   源点选择4  （11 + 5 + 10 = 26）  

part1   

d[x] 表示 以 x 为 子树根节点时的   **向下水系流量**   

显然 由 x 的子树 决定  并且是不同子树的累加和   

d[4] = 5 + 10 = 15      

d[x] = $\sum$  min(x -> y 的边权, d[y]);   1 - 4  最多流 13   显然 叶节点 d[] = INTMAX;   取 Min 才不会取错  

part 2

f[x] 表示 以 x 为 源点 的 水系流量 （即要求值）  f[1] = d[1];  

<img src="C:\Users\LWQ\Desktop\Admin\photo\screenshot-1707143118909.png" style="zoom:80%;" />         <img src="C:\Users\LWQ\Desktop\Admin\photo\screenshot-1707143765309.png" style="zoom:80%;" />

假设 从 x 点 到 y 点 进行 源点置换   （x = 2 ,y = 5)  f[x] 已知  （当前 f[2] = 6 + 9 + 1 ) 

y = 5  的 子树 水系流量 不发生变化 （11 + 3 = 14 ）  即 d[y] 

把向上的部分拆成 （5 --- 2  ） （ 2 -- 其余部分） 两方面的 水系流量  

故 向上的水系流量 = min(5 - 2 边权，1 + 9 )  可以发现 对比 f[x] 少了 6  等价于 min(5 - 2边权，d[y] ) ;

f[5] = d[5] + min(5 - 2, f[2] - min(5 - 2, d[5])); 

f[y] = d[y] + min(边权, f[x] - min(边权, d[y]));

注意  这时候 子叶节点 d[] = 0;  要在 part 1 完成后 处理掉 

特例   1 ---2 ----3    呈 链式结构时 且边权 为1   f[2] = d[2] + min(1,f[1] - min(1,d[2]) ) 时 相减为 0  影响取值

所以要在 特判 为 0 时 取边权 作为 Min的 结果 

```c++
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <cstring>
using namespace std;
typedef long long ll;
const int N = 2e6 + 40;
const int p = 1e9 + 7;
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
int father[N],d[N],f[N],du[N];
int n,t;
void dfs(int x) {
    for(int i = head[x]; i ; i = e[i].next) {
        int y = e[i].to;
        if(y == father[x]) continue;
        father[y] = x; 
        dfs(y);
        d[x] += min(e[i].dis,d[y]);
    }
}
void init(int x){
    for(int i = head[x]; i ; i = e[i].next){
        int y = e[i].to;
        if(y == father[x]) continue;
        father[y] = x;
        int t = f[x] - min(e[i].dis,d[y]);
        if(t == 0) t += e[i].dis;
        f[y] = d[y] + min(e[i].dis,t);
        init(y);
    }
}
int main()
{
    cin>>t;
    while(t--) {
        cin>>n;
        for(int i = 1; i <= cnt; i++) {
            e[i].from = e[i].to = e[i].dis = 0;
            e[i].next = head[i] = 0;
            f[i] = d[i] = father[i] = 0;
            du[i] = 0;
        }
        cnt = 0; 
        for(int i = 1; i < n; i++) {
            int a,b,c;
            cin>>a>>b>>c;
            du[a]++; du[b]++;
            add(a,b,c);
            add(b,a,c);
        }
        for(int i = 2; i <= n; i++) if(du[i] == 1) d[i] = p;  
        dfs(1);
        f[1] = d[1];
        for(int i = 2; i <= n; i++) if(du[i] == 1) d[i] = 0;
        init(1);
        int ans = 0;
        for(int i = 1; i <= n; i++) {
            if(ans < f[i]) {
                ans = f[i];
            }
        }
        cout<<ans<<endl;
    }
    return 0;
}

```





**状压DP** 

  	**前置知识   位运算** 

  判断 一个二进制数x 的第 i 位 是否是 1

  if(x & (1 << (i - 1))  > 0)   // 1 后面 添加 i - 1 个 0  再 &  （1 & 1 = 1 ）  

  将一个数字 x 二进制下第 i 位 更改成 1 

  x = x | (1 << (i - 1))  // (1 | 0 = 1           0 | 0  = 0)

  将 一个数字 x 的二进制下 最靠右的 第一个 1  去掉 

  x  = x & (x - 1) 

**期望DP**

