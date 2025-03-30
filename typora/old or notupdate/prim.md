**prim**    

$O(n^2)$ 找最小生成树   适用于稠密图

基本思路： 

将加入最小生成树的点看作一个集合  

那么寻找最小生成树的过程就是扩展集合。。     扩展集合时 找**距离这个集合最近的，在外面的点**  将其加入集合

 从1开始扩展， 那么把与1相连的点 的$d$  改为边权，而非原设定的最大值，可以做到只搜相邻的,距离最近的。

```c++

struct node{
    int v,w;
};

std::vector<node> e[N];
int cnt = 0,ans = 0;

bool prim(int n, int s) {
    std::vector<int> d(n+1);
    for(int i = 0; i <= n; i++) d[i] = inf;
    d[s] = 0;
    std::vector<bool> vis(N,false);
    for(int i = 1; i <= n; i++) {
        int u = 0;
        for(int j = 1; j <= n; j++) {
            if(!vis[j] && d[j] < d[u] ) u = j;
        }
        vis[u] = true;
        ans += d[u];
        if(d[u] != inf) cnt++;
        for(auto ed : e[u]) {
            int v = ed.v,w = ed.w;
            if(d[v] > w) d[v] = w;
        } 
    }
    return cnt == n;
}
void solve()
{
    int n,m;
    std::cin >> n >> m;
    for(int i = 1,x,y,z; i <= m; i++) {
        std::cin >> x >> y >> z;
        e[x].push_back({y,z});
        e[y].push_back({x,z});
    }
    if(prim(n,1)) std::cout << ans << "\n";
    else std::cout << "orz" << "\n";
    
    return;
}

```

**prim _  heap**  优先队列优化    $O(mlogn)$

基于$Dijkstra$ 的贪心

```c++

bool prim(int n, int s) {
    std::vector<int> d(n+1);
    for(int i = 0; i <= n; i++) d[i] = inf;
    d[s] = 0;
    std::vector<bool> vis(N,false);
    std::priority_queue< std::pair<int,int > > q;
    q.push({0,s});
    while(!q.empty()) {
        int u = q.top().second;
        q.pop();
        if(vis[u]) continue;
        vis[u] = true;
        ans += d[u]; cnt++;
        for(auto ed : e[u]) {
            int v = ed.v,w = ed.w;
            if(d[v] > w) {
                d[v] = w;
                q.push({-d[v],v});
            }
        }
    }
    return cnt == n;
}
```

