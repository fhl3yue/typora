**Dijkstra + 堆优化** 

$O(nlogn)$  + **单源多点最短路径 ** + **仅含有正边权**

**以链式前向星 连有向边建图** 

```c++
struct node{
    int dis;
    int pos;
    bool operator <(const node &x)const
    {
        return x.dis < dis;
    }
};
priority_queue<node> q;
void Dijkstra(int u)
{
     memset(mapp,0x3f,sizeof(mapp));
     memset(vis,0,sizeof(vis));
     mapp[u] = 0;
     q.push((node){0,u});
     while(!q.empty())
     {
         node p = q.top();
         q.pop();
         int x = p.pos;
         if(vis[x]) continue;
         vis[x] = 1;
         for(int i=head[x];i;i=e[i].next)
         {
            int y = e[i].to;
            if(mapp[y] > mapp[x] + e[i].dis)
            {
               mapp[y] = mapp[x] + e[i].dis;
               q.push((node){mapp[y],y});
            }
         }
     }
}
```



**vis数组仅表示有无访问过，不同于SPFA的 是否在队列** 

那么同样可以用来实现对 **矩阵类问题**求解最短路 

已知起点$S$ ，终点$V$  ,

```c++
3 3 3
S01
292
20T
```

**最短路为3**

```c++
    node u = s,v = t;
    memset(f,0x3f,sizeof(f));
    memset(vis,0,sizeof(vis));
    priority_queue<node> q;
    q.push(u);
    f[u.x][u.y] = u.w;
    while(!q.empty()) {
        node t = q.top();
        q.pop();
        if(vis[t.x][t.y] ) continue;
        vis[t.x][t.y] = true;
        for(int i = 0;  i < 4; i++) {
            int tx = t.x + dx[i];
            int ty = t.y + dy[i];
            if(tx > n || tx < 1 || ty > m || ty < 1) continue;
            if(tx == v.x && ty == v.y) {
                f[tx][ty] = min(f[tx][ty],f[t.x][t.y]);
            }
            if(f[tx][ty] > f[t.x][t.y] + w[tx][ty]) {
                f[tx][ty] = f[t.x][t.y] + w[tx][ty];
                q.push({f[tx][ty],tx,ty});
            }
        }
    }
    if(f[v.x][v.y] < val) {
        printf("Yes\n");
    }  else printf("No\n");
```

**着重注意第16-18行** 