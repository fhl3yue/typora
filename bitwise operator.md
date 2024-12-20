**位运算**   

位运算的概念：  

分为逻辑位运算符 和 位移运算符  

**按位与**  

**&  (都 1 为 1)      and**     

**显而易见   $a_1$ and $a_2$ and $a_n$   越and越小**

```
 0 1 1 0 1 0 1

 1 0 1 1 0 1 1

= 0 0 1 0 0 0 1


a & 0 = 0;
a & a = a;
a & ~a = 0;
满足结合律和交换律
```

**按位或**  

**|   (有 1 为 1 )    or     越or值越大   每一位都越趋向于1**  

```
 1 0 0 1 1 0 1

 0 1 1 0 1 0 0 

= 1 1 1 1 1 0 1  

任何数或0 得到它本身
a | 0 = a;
a | a = a;
a | ~a  = 0;
或满足结合律交换律
```



**按位异或**  

**$\oplus$ (不 同 为 1,相 同 为 0)   Xor   ^**  

```
 1 0 1 0 1 0 1

 0 1 0 1 1 1 0

= 1 1 1 1 0 1 1

任何数异或0 得到它本身  
a ^ 0 = a; 
相同的数异或得到0
a ^ a = 0;
异或满足结合律交换律  
a ^ (b ^ c) = (a ^ b) ^ c;
a ^ b = b ^ a;

0 ^ 1 ^ 2 ^ 3 = 0  
(4k,4k+1,4k+2,4k+3)  
```

**按位取反**  

**~ （0 -> 1, 1 -> 0) **

```
 1 0 1 0 1 0 1 

 ~

= 0 1 0 1 0 1 0
```

**左移 <<**  

```
 1 0 0 1 0 1

左移一位  (相当于十进制数 * 2 ) 

1 0 0 1 0 1 0  

n <<= i; // n 左移 i 位， n = n * (2 ^ i);
```

**右移 >>** 

```
 1 0 0 1 1 0 

右移一位  (相当于十进制数 / 2)  

  1 0 0 1 1 

n >>= i; // n 右移 i位，n = n / (2 ^ i);  
```

**分配律的运算** 

```
a & (b | c) = (a & b) | (a & c);
a ^ (b | c) = (a ^ b) | (a ^ c);
a & (b ^ c) = (a & b) ^ (a & c);

false:  a ^ (b & c) = (a ^ b) & (a ^ c);
```

**其他性质**

```c++
a | (a & b) = a;
a & (a | b) = a;

求 n 的 第 k 位 数字  ：   ( n >> k ) & 1
将 n 的 第 k 位 数字 置为1 ： n | (1 << k) 
将 n 的 第 k 位 数字 取反 ： n ^ (1 << k)
判断 n 奇偶性 ：  n & 1 (真为奇，假为偶)
将 n 二进制中最右侧的0 置为 1 :    n | (n + 1) 
将 n 二进制中最右侧的1 置为 0 :    n & (n - 1)
```





 