小红拿到了一个01串，但其中有一些被'?'字符代替。  小红希望将'?'替换成'0'或者'1'字符，使得该串表示的正整数是13的倍数。你能帮小红求出有多少种方案吗？  由于答案过大，请对$10^9+7$取模

这是一个标准的**数位 DP** 问题，主要目的是处理带有不确定数字（`?`）的数字字符串，计算满足某个约束条件的所有方案数。

在本题中，`dp[i][r]` 表示**前 i 位**的数字构成的数对 `13` 取余为 `r` 的方案数。

初始时，`dp[0][0] = 1`，表示没有数字时，对 `13` 取模结果为 `0`。

`dp[n][0]`：表示长度为 `n` 的字符串 `s`，构成的数对 `13` 取模结果为 `0` 的方案数。

余数递推原理：   $AB$ 数,$B$ 仅一位， $AB = A * 10 + B$   

​							$AB$ `%` 13 = ($A$ `%` 13 * 10 + B) `%` 13

$dp[i+1][(r*10+V)mod\quad13] += dp[i][r]$ 

```
#include <iostream>
#include <vector>
#include <string>
#include <cstring>
using namespace std;

const int MOD = 1e9 + 7;

int solve(const string& s) {
    int n = s.length();
    vector<vector<int>> dp(n + 1, vector<int>(13, 0));
    dp[0][0] = 1;

    for (int i = 0; i < n; ++i) {
        for (int r = 0; r < 13; ++r) {
            if (dp[i][r] == 0) continue;
            if (s[i] == '?') {
                dp[i + 1][(r * 10 + 0) % 13] = (dp[i + 1][(r * 10 + 0) % 13] + dp[i][r]) % MOD;
                dp[i + 1][(r * 10 + 1) % 13] = (dp[i + 1][(r * 10 + 1) % 13] + dp[i][r]) % MOD;
            } else {
                int val = s[i] - '0';
                dp[i + 1][(r * 10 + val) % 13] = (dp[i + 1][(r * 10 + val) % 13] + dp[i][r]) % MOD;
            }
        }
    }

    return dp[n][0]; 
}

int main() {
    string s;
    cin >> s;
    cout << solve(s) << endl;
    return 0;
}

```

小红拿到了一个01串，她初始站在第一个字符。小红可以进行以下移动方式：  
1\. 花费$x$能量，移动到当前位置右边、离当前位置最近的，和当前字符相同的字符；  
2\. 花费$y$能量，移动到当前位置右边、离当前位置最近的，和当前字符不同的字符。  

小红想知道，她移动到最右端的最小花费是多少？



这道题与一些经典DP问题有类似之处：

- **线性DP**：状态 `dp[i]` 线性地依赖于前面的状态。

- **跳跃DP**：类似于青蛙跳台阶问题，但跳跃的代价（`x` 和 `y`）取决于字符条件。

- **图上的最短路径问题**：可以将字符串的每个位置看成图中的一个节点，跳跃操作看成带权重的边，目标是找到从起点到终点的最短路径。

  `dp[i]`：从起点（`0`）到达位置 `i` 的最小代价。

  **状态转移**
  从位置 `i` 跳到：

  - **相同字符** 的位置 `S[i]`： $dp[S[i]]=min⁡(dp[S[i]],dp[i]+x)$
  - **不同字符** 的位置 `D[i]`： $dp[D[i]]=min⁡(dp[D[i]],dp[i]+y)$

  **边界条件**

  - 初始状态：`dp[0] = 0`（起点代价为0）。
  - 其余位置：`dp[i] = LLONG_MAX`（未到达的位置初始化为无穷大）。

  **最终目标**
  `dp[n-1]`：字符串末尾位置的最小代价。

  是否存在与当前字符相同的下一个位置 `S[i]`,存在与当前字符不同的下一个位置 `D[i]`  需要预处理找到

  ```c++
  #include <iostream>
  #include <vector>
  #include <unordered_map>
  #include <climits>
  typedef long long ll;
  using namespace std;
  
  ll solve(int n, int x, int y, const string& s) {
      vector<ll> dp(n, LLONG_MAX);  // 使用LLONG_MAX确保long long类型
      dp[0] = 0;  // 初始状态
  
      vector<int> S(n, -1);  // S[i]: 跳到相同字符的位置
      vector<int> D(n, -1);  // D[i]: 跳到不同字符的位置
  
      unordered_map<char, int> mp;  // 记录字符最近出现的位置
  
      // 预处理S[i]和D[i]
      for (int i = n - 1; i >= 0; --i) {
          // 更新S[i]
          if (mp.count(s[i])) {
              S[i] = mp[s[i]];  // 相同字符的最近位置
          }
          mp[s[i]] = i;
  
          // 更新D[i]: 跳到不同字符
          for (char ch = '0'; ch <= '1'; ++ch) {
              if (ch != s[i] && mp.count(ch)) {
                  D[i] = mp[ch];  // 找到不同字符的最近位置
                  break;
              }
          }
      }
  
      for (int i = 0; i < n; ++i) {
          if (dp[i] == LLONG_MAX) continue;
          if (S[i] != -1) {
              dp[S[i]] = min(dp[S[i]], dp[i] + x);
          }
          if (D[i] != -1) {
              dp[D[i]] = min(dp[D[i]], dp[i] + y);
          }
      }
  
      return dp[n - 1];
  }
  
  int main() {
      ios::sync_with_stdio(false);
      cin.tie(nullptr);
  
      int n, x, y;
      string s;
      cin >> n >> x >> y >> s;
      cout << solve(n, x, y, s) << '\n';
      return 0;
  }
  
  ```

  
