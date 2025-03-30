### BFS

有一个包含 $H$ 水平线和 $W$ 纵列的网格。让 $(i, j)$ 表示从顶部开始的 $i$ \第一行 $(1\leq i\leq H)$ 和从左侧开始的 $j$ \第列 $(1\leq j\leq W)$ 处的单元格。

最初，在细胞 $(i,j)$ 中有一个强度为 $S _ {i,j}$ 的黏液，A就是细胞 $(P,Q)$ 中的黏液。

在执行以下动作任意次数（可能为零）后，找到A的最大可能力量：

-在与他相邻的黏液中，选择一个强度严格小于他自身强度的 $\dfrac{1}{X}$ 倍的黏液吸收。结果，被吸收的黏液消失了，高桥的强度随着被吸收黏液的强度而增加。

在执行上述动作时，消失的黏液所留下的空隙立即被A填满，与消失的黏液相邻的黏液（如果有的话）成为新的与A相邻的黏液。

- $1\leq H,W\leq500$

- $1\leq P\leq H$

- $1\leq Q\leq W$

- $1\leq X\leq10^9$

- $1\leq S _ {i,j}\leq10^{12}$

- All input values are integers.

  两个点：  优先队列选最小的先吸收， 128控制范围， $BFS$

  ```c++
  #include <bits/stdc++.h>
  typedef long long ll;
  using namespace std;
  using i128 = __int128;
  
  const int dx[] = {0, 0, -1, 1};
  const int dy[] = {-1, 1, 0, 0};
  
  i128 read() {
      i128 flag = 1, num = 0;
      char cum = getchar();
      while (cum < '0' || cum > '9') {
          if (cum == '-') flag = -1;
          cum = getchar();
      }
      while (cum >= '0' && cum <= '9') {
          num = (num << 3) + (num << 1) + (cum - '0');
          cum = getchar();
      }
      return flag * num;
  }
  std::ostream &operator<<(std::ostream &os, i128 n) {
      if (n == 0) return os << "0";
      if (n < 0) {
          os << "-";
          n = -n;
      }
      std::string s;
      while (n) {
          s += '0' + n % 10;
          n /= 10;
      }
      std::reverse(s.begin(), s.end());
      return os << s;
  }
  struct Node {
      ll x, y, sw;
      bool operator<(const Node &other) const {
          return sw > other.sw;
      }
  };
  void solve() {
  	ll H, W, X;
      ll P, Q;
      std::cin >> H >> W >> X >> P >> Q;
      P--, Q--;
  
      vector<vector<ll>> S(H, vector<ll>(W));
      for (int i = 0; i < H; ++i) {
          for (int j = 0; j < W; ++j) {
              std::cin >> S[i][j];
          }
      }
  
      priority_queue<Node> q;
      vector<vector<bool>> vis(H, vector<bool>(W, false));
      i128 ans = S[P][Q];
      vis[P][Q] = true;
  
      //q.insert({P, Q, S[P][Q]});
      for(int k = 0; k < 4; k++) {
      	int sx = P + dx[k], sy = Q + dy[k];
      	if ((sx < 0) || (sx >= H) || (sy < 0) || (sy >= W) || (vis[sx][sy])) continue;
      	q.push({sx,sy,S[sx][sy]});
      	vis[sx][sy] = true;
      }
      while (!q.empty()) {
          Node cur = q.top();
          int x = cur.x, y = cur.y, sw = cur.sw;
          if(i128(S[x][y]) * i128(X) >= i128(ans))  break;
  		q.pop();
  		ans += S[x][y];
          for (int d = 0; d < 4; ++d) {
              int nx = x + dx[d];
              int ny = y + dy[d];
              if ((nx < 0) || (nx >= H) || (ny < 0) || (ny >= W)) continue;
              if (vis[nx][ny]) continue;
              q.push({nx,ny,S[nx][ny]});
              vis[nx][ny] = true;
      	}
  	}
      cout << ans << '\n';
  	return;
  }
  
  ```

  