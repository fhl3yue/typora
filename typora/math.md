

**等差数列**   

$a_{n} = a_{1} + (n-1) d$  

 $s_{n} = \frac{n(a_{1} + a_{n})}{2} =  na_{1} + \frac{n(n-1)}{2} d$   

**等比数列**

$a_{n} = a_{1} q^{n-1}$

$s_n = \frac{a_{1} (1 - q^{n})}{1-q}$ 

 **乘法逆元**

对于任意整数 $a$ 而言，如果 $a$ 和 $p$ 互质，存在一个整数 $x$ 使得 $a \times x \equiv 1(\bmod p)$    

​	$x$ 为 $a$ 在 模 $p$ 意义下的乘法逆元 ，记为$a^{-1}$   

**不定方程$ax + by = 1$  有解的充要条件是 $a,b$ 互质。**

**费马小定理**: 若 $p$ 是质数，对任意整数 $a$ 不是 $p$ 的倍数，有 $a^{p-1} \equiv 1(\bmod p)$ ，也可以写作 $a^{p} \equiv$ $a(\bmod p)$ 。  

证明: 根据同余的性质， $a, 2 a, 3 a \ldots \ldots,(p-1) a$ 分别 $\bmod p$ 的结果各不相同。那么:  
$$
\begin{aligned}  
a \times 2 a \times 3 a \ldots \ldots \times(p-1) a & \equiv 1 \times 2 \times 3 \ldots \ldots \times(p-1) & (\bmod p) \\  
a^{p-1} \times[1 \times 2 \times 3 \ldots \ldots \times(p-1)] & \equiv 1 \times 2 \times 3 \ldots \ldots \times(p-1) & (\bmod p) \\  
a^{p-1} & \equiv 1 \quad(\bmod p) &  
\end{aligned}  
$$

如何求**乘法逆元**：若 $p$ 是质数，则有 $a^{p-1} \equiv 1(\bmod p)$ ，而 $a \times x \equiv 1(\bmod p)$ ，所以 $a^{p-2}$ 是 $a$ 模 $p$ 意义下的的乘法逆元。  

可以用**快速幂**，时间复杂度为 **$O(\log p)$** 

**扩展欧几里得**  $ax + by = gcd(a,b)$ 

$gcd(a,b)$ = $ax  + by$ 

$gcd(b,a\%b)$  = $bx_{1} + (a \% b) y_{1}$

​						= $bx_{1} + (a - [a / b] * b)y_{1}$

​						=$ay_{1}$  + $b(x_{1} - [a/b]y_{1})$

$x = y_{1}$ ,   $y = x_{1} - [a/b]y_{1}$

```
ll exgcd(ll a,ll b,ll &x,ll &y)
{
	if(b == 0)
	{
	   x = 1;
	   y = 0;
	   return a;
	}
	ll d,x1,y1;
	d = exgcd(b,a%b,x1,y1);
	x = y1;
	y = x1 - a / b * y1;
	return d;
}
```

 若$ax + by = c$   ($c$  为 $gcd(a,b)$  的 倍数)      答案为 $x$ * $gcd(a,b)$ 

**通解**

$x = x_{0} + \frac{b}{gcd(a,b)} * k$ 

$y = y_{0}  - \frac{a}{gcd(a,b)}  * k$  

**证明**

$a(x + n) + b(y - m) = c$

$ax + by + an - bm = c$ 

$an - bm = 0   \\an = bm  $

$\frac{a}{gcd(a,b)}*n = \frac{b}{gcd(a,b)} * m$ 

$a'n = b'm   \\gcd(a',b') = 1 \\n = b' = b/gcd(a,b)\\ m = a' = a/gcd(a,b)$  

**斐波那契数列**

$1,1,2,3,5,8,13...$

$S_n = Fib(n+2) - 1$ 

**gcd 与 斐波那契** 

$gcd(F_n,F_m) = F_{gcd(n,m)}$

**递推求逆元** 

给定$n,p$  ,求 1~$n$  在 模 $p$ 意义下的逆元 ，$p$ 为 质数

$inv[1] = 1;$

$inv[i] = (p - [p/i] * inv[p\%i]) \% p;$

**阶乘逆元**

给定$n$,求 1~$n$ 每个数阶乘在模$p$ 意义下的逆元

$f(n-1)^{-1} = f(n)^{-1} * n$

**算术基本定理**

**N = $p_{1}^{a_{1}} * p_{2} ^ {a_{2}}$ $\ldots$ $*p_{i} ^ {a_{i}}$ ($p_{i}$ 为质数)** 

**那么**

**N 的 约数个数 ：**    **$\sigma$(N) =  (1 + $a_{1}$) * (1 + $a_{2}$) * (1 + $a_{3}$) * **$\ldots$**(1 + $a_{i}$)** 

**N  的各约数之和 ：** **$\mu$(N) =  (1 + $p_{1}^{1}$ + $p_{1}^{2}$**  + $\ldots$  $p_{1}^{a1}$)  *  (1 + $p_{2}^{1}$ + $p_{2}^{2}$**  + $\ldots$  $p_{2}^{a2}$)  * $\ldots$ * **(1 + $p_{i}^{1}$ + $p_{i}^{2}$**  + $\ldots$  $p_{i}^{ai}$))

**N 的 约数 的 d 次方 之和**  ：  就是把上式   $p1 = p1 ^ d$     注意 $d = 0$   就变成了 约数个数

**N ！**  **进行算术基本定理的分解**

1.  找到 **1~N** 中 质数 
2.  **每个质数 的指数 ： **  $\frac{N}{prime[i] ^{1}}$ + $\frac{N}{prime[i]^{2}}$  + $\ldots$   直至  N <  $prime[i]^{m}$ ,除出结果为0     

**组合数取模**

**$C^{m}_{n}$ =  $\frac{n!}{(n-m)!m!}$**     **(乘法逆元  取模  m <= n < $10^{5}$)   模为大质数 费马小定理   合数为exgcd **

**$C^{m}_{n}$  = **   $C^{m}_{n-1}$  + $C^{m-1}_{n-1}$    **（预处理  递推打标取模  m <= n < 2000）**

**Lucas 定理**       $C^{m}_{n}$ % p  =  $C^{m/p}_{n/p}$  *****  $C^{m\%p }_{n\%p}$  $\%$ p    (n , m < $10^{18}$, (质数)p < $10^{5}$)
[动态更改模数的取模模板类](https://www.luogu.com.cn/record/211600349)

```c++

template<int MOD>
class Comb {
public:
    int n;
    std::vector<i64> _fac;    // 阶乘数组
    std::vector<i64> _invfac; // 逆阶乘数组
    std::vector<i64> _inv;    // 数字的逆元
    Comb() : n(0), _fac(1, 1), _invfac(1, 1), _inv(1, 0) {}
    Comb(int n) : Comb() {
        init(n);
    }
    static i64 ksm(i64 a, i64 b) {
        i64 res = 1;
        while (b) {
            if (b & 1) res = res * a % MOD;
            a = a * a % MOD;
            b >>= 1;
        }
        return res;
    }

    static i64 modinv(i64 a) {
        return ksm(a, MOD - 2);
    }
    void init(int m) {
        m = std::min(m, MOD - 1);
        if (m <= n) return;
        _fac.resize(m + 1);
        _invfac.resize(m + 1);
        _inv.resize(m + 1);
        for (int i = n + 1; i <= m; i++) {
            _fac[i] = (_fac[i - 1] * i) % MOD;
        }
        _invfac[m] = modinv(_fac[m]);
        for (int i = m; i > n; i--) {
            _invfac[i - 1] = (_invfac[i] * i) % MOD;
            _inv[i] = (_invfac[i] * _fac[i - 1]) % MOD;
        }
        n = m;
    }
    i64 fac(int m) {
        if (m > n) init(2 * m);
        return _fac[m];
    }
    i64 invfac(int m) {
        if (m > n) init(2 * m);
        return _invfac[m];
    }
    i64 inv(int m) {
        if (m > n) init(2 * m);
        return _inv[m];
    }
    //C(n, m) % MOD
    i64 binom(int n, int m) {
        if (n < m || m < 0) return 0;
        return (fac(n) * invfac(m) % MOD) * invfac(n - m) % MOD;
    }
    i64 lucas(i64 n, i64 m) {
        i64 p = MOD;
        if(n < p && m < p) return binom(n,m);
        return binom(n%p,m%p) * lucas(n/p,m/p) % p;
    }
};

```

 $C^{0}_{n}$  = 1; 



$x^{2} \equiv 1(mod \ kn)$  $k \le n$ 

$1 \le n\le \ 200000000$

求$x$,并从小到大输出 

**根据质因子 找到各个因数**

```c++
vector<pair<int,int>> getPrimeFactors(ll x) {
	vector< pair<int,int> > v;
	for(int i = 2; i * i * 1ll <= x; i++) {
		int num = 0;
		if(x % i == 0) {
			while(1) {
				x /= i;
				num++;
				if(x % i != 0) break;
			}
			v.push_back({i,num});
		}
	}
	if(x > 1) v.push_back({x,1});
	return v; 
} 
vector<ll> getAllFactorsDP(ll x) {
    vector< pair<int,int> > primeFactors = getPrimeFactors(x);
    vector<ll> factors;
    int size = primeFactors.size();
    vector<vector<ll>> dp(size+1);
    dp[size].push_back(1);
    for (int i = size-1; i >= 0; i--) {
        vector<ll> tmp = dp[i+1];
        ll p = primeFactors[i].first;
        ll count = primeFactors[i].second;
        for (int j = 0; j <= count; j++) {
            for (ll path : tmp) {
                dp[i].push_back(path * pow(p, j));
            }
        }
    }
    return dp[0];
}
```



**$O(logn)$ 筛质因子** 

$mindiv[]$  表示一个数最小的质因子 

能够在 线性筛的过程中全部找出来$mindiv$ 

  

```c++

int plist[N];
int mindiv[N * 10];
bool not_prime[N * 10];
void init() {
    int T = 1e7;
    int cnt = 0;
    mindiv[1] = 1;
    for(int i = 2;i <= T; i ++) {
        if(not_prime[i] == false) {
            plist[++ cnt] = i;
            mindiv[i] = i;
        }
        for(int j = 1; j <= cnt; j ++) {
            int x = i * plist[j];
            if(x > T) break;
            not_prime[x] = true;
            mindiv[x] = plist[j];
            if(i % plist[j] == 0) break;
        }
    }
    return;
}
void solve() {
    scanf("%d",&n);
    while(n != 1) {
        int div = mindiv[n];
        if(mindiv[n] == div) {
            printf("%d ", div);
            while(mindiv[n] == div) {
                n /= div;
            }
        }
    }
    printf("\n");
    return;
}


```

**约瑟夫环数学解**

求最后剩下人的编号  

```c++
int fun(int n, int m) {
	return n == 1 ? n : (fun(n - 1, m) + m - 1) % n + 1;
}
```



  **欧拉函数**

对于一个正整数$n$,$\phi(n)$ 表示 $1-n$ 与$n$互质的数的个数

1. $n$为质数，$\phi(n) = n - 1$ 

2. $\phi(n) = n * (\frac{p-1}{p})$  $p$ 表示 $n$的质因子 

3.  $\phi(p * q) = \phi(p) * \phi(q) $  当且仅当 $p,q$ 均为质数

4. 筛法求$\phi$ 

   ```c++
   void euler(int n)//nlogn
   {
       for(int i = 1;i <= n;i++) phi[i] = i;
       for(int i = 2;i <= n;i++)
       {
           if(phi[i] == i)
           {
               for(int j = i;j <= n;j += i)
               phi[j] = phi[j] / i * (i - 1);
           }
       }
   }
   ```

   ```c++
   void euler(int n)
   {
       phi[1] = 1;
       for(int i=2;i<=n;i++)
       {
           if(not_prime[i] == 0) plist[++cnt] = i,phi[i] = i-1;
           for(int j=1;j<=cnt;j++)
           {
               int x = i * plist[j];
               if(x > n) break;
               not_prime[x] = 1;
               if(i % plist[j] == 0)
               {
                    phi[x] = phi[i] * plist[j];
                    break;
               }
               else phi[x] = phi[i] * (plist[j] - 1);
           }
       }
   }
   ```

   欧拉公式的延伸：对于一个数，与其互质的数的总和是$euler(n)*n/2$。
   
   $\sum_{i=1}^{n} i[gcd(i,n) = 1] = euler(n) * n / 2$
   
   **整除分块**
   
   ![](https://cdn.luogu.com.cn/upload/image_hosting/lujac7y6.png)
   
   **积性函数**
   
   ![](https://cdn.luogu.com.cn/upload/image_hosting/212087cf.png)
   
   ![](https://cdn.luogu.com.cn/upload/image_hosting/zubfm66q.png)
   
   ![](https://cdn.luogu.com.cn/upload/image_hosting/759suedg.png)
   
   
