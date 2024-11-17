**Crying 正在学习初中数学。 今天他学到了如何化简 $\sqrt{n}$ ，其中 $n$ 是一个正整数。他想到，如果给出一个很大的 $N$ ，要求你化简所有 $\sqrt{n}$ ，其中 $n=1,2, \ldots, N$ ，这个问题就会变得稍微有趣一点。 为了显得善良一些，若 $\sqrt{n}$ 化简为 $a_{n} \sqrt{b_{n}}$ ，则你只需要求出  $\sum_{n=1}^{N}\left(a_{n}+b_{n}\right) \bmod 2^{64}$  
其中称 $\sqrt{n}$ 化简为 $a_{n} \sqrt{b_{n}}$ 当且仅当 $\left(a_{n}, b_{n}\right)$ 在所有满足 $\sqrt{n}=a \sqrt{b}$ 的正整数对 $(a, b)$ 中是 $a$ 最大的那个。**

**输入描述**

第一行，一个正整数 $N$

$1 \le N \le 1.5 \times 10 ^{16}$

**样例1**

```
5
18
```

**样例2**

```
10000000

32898926882292
```





Crying 在面对错误码 404 Not Found。  
他有一个 $\{0,1, \ldots, n-1\}$ 的排列 $\pi_{1}, \pi_{2}, \ldots, \pi_{n}$ 。他每次会在一个区间里尝试找数，但总是找不到。所以他需要你来帮他解决一些问题。  

他会进行 $m$ 次询问，每次询问给出 $l, r, k$ ，意味着他希望你告诉他第 $k$ 小的不能在集合 $\left\{\pi_{l}, \pi_{l+1}, \ldots, \pi_{r}\right\}$ 中找到的自然数。

输入描述:

第一行, 两个正整数 $n, m$ 。
第二行, $n$ 个非负整数 $\pi_{1}, \pi_{2}, \ldots, \pi_{n}$ 。
以下 $m$ 行, 每行三个正整数 $l, r, k$ 。
对于所有数据, 保证 $1 \leq n, m \leq 5 \times 10^{5}, 0 \leq \pi_{i}<n$, 所有 $\pi_{i}$ 互不相同, $1 \leq l \leq r \leq n, 1 \leq k \leq 10^{18}$ 

输出描述:
$m$ 行, 每行一个非负整数, 依次表示每次询问的答案。

```
5 7
0 4 2 1 3
1 3 1
1 3 2
1 3 3
2 3 3
2 3 4
2 3 10
2 3 1000
```

```
1
3
5
3
5
11
1001
```


​	小红拿到了一个数组，她准备选择若干元素乘以 -1 ，使得最终所有元素的和为 0 。小红想知道最少需要	选择多少个元素?

输入描述:

第一行输入一个正整数 n, 代表数组的大小。
		第二行输入 n 个整数 $a_{i}$, 代表数组的元素。
 			$1 ≤ n ≤ 200$
			$-200 ≤ a_{i} ≤ 200$

输出描述:

如果无法使得最终所有元素之和为 0 , 则输出 -1 。
		否则输出一个整数, 代表选择元素的最小数量。

```
3
1 -2 3

1
```



小笨有一个长为 $n$ 的数组 $a$ ，他想知道有多少个 $(i, j)(1 \leq i, j \leq n)$ 满足 $lcm\left(a_{i}, a_{j}\right)=a_{i} \oplus a_{j}$ 。

$n \le  2 *10 ^{5}$   $a_{i} \le 10^{9}$  

```c++
if(a[i] == 0) cnt++;

cout<<cnt * cnt;
```

给你一个长为n的序列a，m次查询区间[l,r]内出现次数第k1小的数中值第k2小的数是多少？

[]([数列查找 (nowcoder.com)](https://ac.nowcoder.com/acm/problem/14896))





**第k大回文数 **   $1 \le k \le 10^{18}$   []([D - Palindromic Number (atcoder.jp)](https://atcoder.jp/contests/abc363/tasks/abc363_d))



$N \le 20  , a[i] \le 10^8$  分成两部分，使得两者最大值最小可能值是多少 [C - Separated Lunch (atcoder.jp)](https://atcoder.jp/contests/abc374/tasks/abc374_c)

         ```c++
         	void dfs (int id, ll now){
         		if(id >= n) {
         			ans = std::min(ans,std::max(now,z - now));
         			return;
         		}
         		dfs(id + 1,now + a[id]);
         		dfs(id + 1,now);
         	}
         ```

爆搜  $O(N2^{N})$   如果$N$ 范围扩大又该如何？ 01背包？

