## STL 与 库函数   
### 1. Vector 的了解
std::vector: 内存连续的，可以动态分配内存，很多时候我们不能提前开好那么大的空间,（例如预处理 1 ~ n 中 所有数的约数），我们就需要得到可变长度数组，这就是vector。  vector还能够实现线性复杂度的插入删除，常数复杂度的随机访问。       
std::vector 重载了比较运算符和赋值运算符,这使得我们可以方便的判断两个容器是否相等，此外std::vector还重载了赋值运算符,使得数组拷贝更加方便。   
std::vector 重载了 = 运算符，所以我们方便的初始化，此外从C++11起，std::vector还支持列表初始化。例如: std::vector<int> data{1,2,3};    

### 2. vector 常用函数 
```   
std::vector<int> v; 
std::vector<std::vector<int>> g;
v.empty();  // 返回一个bool 值，即v.begin() == v.end(),true 为 空，反之为 非空。    
v.size();  // 返回容器长度（元素数量）    
v.push_back(x); //  在末尾插入一个元素。均摊复杂度为常数。    
v.pop_back();// 删除末尾元素      
v.insert(pos,x);//在pos 的位置，插入x;
lower_bound(); // 返回指向首个大于等于给定元素的迭代器，如果不存在返回end();// 要求序列有序 
upper_bound(); // 返回指向首个大于给定元素的迭代器，如果不存在返回end();     
int q = std::upper_bound(v.begin(),v.end(),A) - v.begin();
lower_bound与upper_bound()查找一个元素的时间复杂度为O(log n);     
insert（）在大部分情况下，时间复杂度都为O（1）。只有个别情况下，复杂度才比较高，为O（n）      
v.insert(upper_bound(v.begin(),v.end(),a),a);     
v.clear(); // 清空std::vector    
v.erase(~~); // 删除某个迭代器 或区间内元素。     
```
关于 v.erase() 的例子:    
例如此时需要对std::vector中的元素去重，你可以这样写   

```
std::sort(v.begin(),v.end());
v.erase(std::unique(v.begin(),v.end()),v.end());  // 将重复的移动至末尾,并将其删除。  
```
vector 中 使用 pair 的例子：     
例如需要对已经存入的坐标按照x值升序排列，你可以这样写   
```c++
vector< pair<int,int> > vec;
vec.push_back({u,v});
bool cmp(pair<int,int> a, pair<int,int> b)
{
    if(a.first == b.first) retun a.second < b.second;
    return a.first < b.first;
}
sort(vec.begin(),vec.end(),cmp);
for(auto it = vec.begin() ; it = vec.end(); it ++)
{
    cout<<it->first << " " <<it->second;
    printf("\n");
}
```
**sort** $sort(v.begin(),v.end())$

```c++
is_sorted(v.begin(),v.end()); // 返回 是否为升序排列 true or false
is_sorted(v.rbegin(),v.rend());// 返回 是否为降序排列 true or false
```

**二维都变长的二维容器数组**

**1、在C++中,可以这样初始化一个二维vector数组并指定大小:**

cpp
vector<vector<int>> vec(3, vector<int>(4));

这个代码会创建一个3行4列的二维vector数组,每个元素初始化为0:

vec =   
\[0 0 0 0\]  
\[0 0 0 0\]   
\[0 0 0 0\]

**2、你也可以在初始化时指定每个元素的值:**

cpp
vector<vector<int>> vec(3, vector<int>(4, 1)); 

这个会创建一个3行4列的二维vector,每个元素初始化为1:

vec =   
\[1 1 1 1\]  
\[1 1 1 1\]  
\[1 1 1 1\]

**3、如果你想指定每个vector的大小,并手动初始化每个元素,可以这样写:**

cpp
vector<vector<int>> vec;
vec.resize(3);        // 3行

vec\[0\].resize(4);     // 第一行4列
vec\[0\] = {1, 2, 3, 4};

vec\[1\].resize(2);     // 第二行2列 
vec\[1\] = {5, 6};  

vec\[2\].resize(3);     // 第三行3列
vec\[2\] = {7, 8, 9}; 

这个会创建:

vec =    
\[1 2 3 4\]  
\[5 6 0 0\]   
\[7 8 9 0\]

**总结**

所以总结一下,初始化一个二维vector数组并指定大小的方法有:

1\. vector<vector<int>> vec(行数, vector<int>(列数));   
2\. vector<vector<int>> vec(行数, vector<int>(列数, 初始值));  
3\. vector<vector<int>> vec; vec.resize(行数); vec\[i\].resize(列数); vec\[i\] = {值};

**一维长度固定，二维长度可变的二维容器数组**

vector<int> v\[n\] n 为第一维的长度

[![复制代码](http://assets.cnblogs.com/images/copycode.gif)](javascript:void(0); "复制代码")

// 初始化一个一维长度为3的vector
vector<vector<int\>> vec(3);

// 为每个一维vector初始化不同长度 
vec\[0\] = vector<int\>(5); 
vec\[1\] = vector<int\>(10);
vec\[2\] = vector<int\>(2);





### 3.Stack（栈）   

std::stack 是一种后进先出(LIFO)的容器，仅支持查询或删除最后一个加入的元素（即栈顶元素），不支持随机访问，且为了保证数据的严格有序性，不支持迭代器。    
常用函数：
```
std::stack<int> stk;
stk.empty();  // 返回一个bool 值，判断栈是否为空,true 为 空，反之为 非空。
stk.push(x); // 向栈顶加入元素x。
stk.top(); // 返回 栈顶元素    
stk.pop(); // 栈顶元素出栈 。     
```
### 4.queue (队列)    
std::queue 是一个队列容器，满足FIFO(先入先出) 的原则。    
常用函数：  
```
std::queue<int> q;
q.empty();  // 返回一个bool 值,true 为 空，反之为 非空。
q.push(x); // 向队尾插入元素x。    
q.front(); // 返回队首元素。
q.back(); // 返回队尾元素。
q.pop(); // 队首元素出队。
q.size(); // 返回一个int 类型的数值，表示队列中元素的个数。

```
### 5.priority_queue     
std::priority_queue 是一个优先队列。顾名思义，也是一个队列容器，它满足std::queue 的所有特性，不同的是，优先队列会将所有的元素按照Compare 排序。     
定义时与std::queue 类似，都需要指明数据类型，优先队列还需要指明Compare的内容，但不指明时默认为std::greater,表示从队首到队尾元素依次为降序排序。    
若数据类型是结构体 node    
由于编译器无法默认的比较两个结构体的大小关系，于是我们需要对小于号 < 进行重载，使之能够对两个结构体变量进行比较：   
```c++
struct node{
    int x; int y;
    bool operator < (const node &a) const
    {
        return x > a.x;
    }
};
std::priority_queue<node> q;

struct cmp {  
    bool operator()(std::pair<ull, ull> a, std::pair<ull, ull> b) {  
        if(a.second == b.second) return a.first > b.first;
        return a.second > b.second;
    }  
}; 
std::priority_queue< std::pair<ull,ull> , std::vector<std::pair<ull,ull>>, cmp> q;
```
常用函数：   
与std::queue基本一致，主要的不同点在于std::priority_queue中，q.top() 表示队首元素。     
### 6.set   
std::set 是一个关联容器，含有键值类型对象的已排序集（集合中元素都是有序的），搜索，移除，插入，拥有对数复杂度。    
与数学中的集合相似，std::set 中不会出现值相同的元素，如果需要有相同元素的集合，需要使用std::multiset,使用方法与std::set基本相同。    
常用函数：    
```c++
std::set<int> s;
s.insert(x); // 当容器中没有等价元素的时候，将元素x插入到std::set 中    
s.erase(x); // 删除值为x的元素，返回一个删除元素的个数。   
s.erase(pos); // 删除迭代器为pos的元素，要求迭代器必需合法；   
s.erase(first,last); // 删除迭代器在[first,last] 范围内的所有元素；    
s.clear(); // 清空std::set    
s.count(x); // 返回std::set内键为x的元素数量。    
s.find(x); // 在std::set内存在键为x的元素时返回该元素的迭代器，否则返回end();     
s.size();// 返回容器内元素个数
s.lower_bound(x); // 返回第一个大于等于x的元素的迭代器
s.rbegin();  // 返回指向最后一个元素的迭代器   排好序的 
```
**multiset** 

插入和删除都是 $O(nlogn)$  的时间复杂度 

在这里介绍一个新函数 **extract**  起到容器内移除作用  

与 **erase ** 不同的是

1. **Efficiency**: `erase` 函数会在删除元素后重新平衡 `multiset`，这可能会导致性能损失，尤其是在循环中频繁删除元素时。而 `extract` 函数可以更高效地从 `multiset` 中提取元素，因为它不需要重新平衡容器。

2. **Correctness**: 在循环中使用 `erase` 函数可能会导致迭代器失效的问题，因为在删除元素后迭代器可能指向无效的位置。而 `extract` 函数返回一个范围，这意味着在提取元素后仍然可以通过范围内的迭代器访问提取的元素，从而避免了这个问题。

3. **Clarity**: 使用 `extract` 函数更清晰地表达了代码的意图，即从 `multiset` 中提取特定的元素，而不是简单地删除它们。

总之，尽管 `erase` 函数也可以用来删除元素，但在这种情况下，使用 `extract` 函数更合适，因为它既更高效也更安全。



### 7.map   

我们都知道一维数组的下标是int类型的数，但是当我们需要记录一个人的姓名出现了几次，第一时间想法一定是，A[name] ++;    
由此，我们需要一个能用各种数据类型作为下标的数组。 map由此产生。    

常用函数：    

```c++
std::map<string,int> mp;
string op;
scanf("%s",)
mp[op]++;


map<ll,ll> dp;
if(dp.count(x)) return dp[x];

std::map<int,int> f;
if(f.contains(x))  c++20
std::map<std::string,std::map<std::string,std::set<std::string>>> mp;
```

### 8.unordered_map

1. **底层实现**：
   - `std::map` 使用红黑树（一种自平衡二叉搜索树）来实现，保证了元素的有序性。在对元素进行迭代或者搜索时，`std::map` 中的元素会按照键的顺序排列。
   - `std::unordered_map` 使用哈希表（一种散列表）来实现，它通过哈希函数将键映射到存储桶中，不保证元素的顺序。哈希表的优势在于快速的查找、插入和删除，但不维护元素的顺序。

2. **性能特征**：
   - `std::map` 的查找、插入和删除操作的时间复杂度是 O(log n)，其中 n 是元素的数量。这是因为红黑树保持了树的平衡性，所以这些操作的性能相对稳定。
   - `std::unordered_map` 的平均情况下，查找、插入和删除操作的时间复杂度是 O(1)，但在最坏情况下可能达到 O(n)。这是因为哈希冲突可能会导致需要线性探测或者链表的长度增加，从而降低性能。

3. **元素顺序**：
   - `std::map` 保持元素的有序性，元素按照键的比较函数的顺序排列。
   - `std::unordered_map` 不保证元素的顺序，元素的存储顺序取决于哈希函数的映射和桶的排列。

4. **空间开销**：
   - 由于红黑树的结构，`std::map` 往往会比 `std::unordered_map` 消耗更多的内存空间。
   - `std::unordered_map` 中哈希表的大小通常会大于其中的元素数量，以减少哈希冲突的发生。因此，`std::unordered_map` 在内存消耗方面可能会更高一些。

在选择使用 `std::map` 还是 `std::unordered_map` 时，需要根据具体的需求来决定。如果需要有序性，或者需要在元素之间进行范围查询，`std::map` 是更好的选择。如果对于查询的速度要求更高，而不关心元素的顺序，`std::unordered_map` 则更适合。

综上 ：  当遇到 用 $10^9$  大小的数 作为 数组下标 时 往往使用 unordered_map  

```c++
#include <unordered_map> 
unordered_map <int,int > f;
//充当 f[N] 的作用
```

### 9.list  

list  底层 以 双向链表的形式  

```
#include <list> 
list <int> List;  
```

**构建 迭代器类型的 变量数组** 

```c++
#include <list> 
using namespace std;
using Iter = list <int> :: iterator;
Iter pos[M];

//同样可以作为  unordered_map 的 变量值类型 
unordered_map< int, List > pos;  
```

**插入 ** 

``` c++
List.push_back(1);
// 将 1 从 后面 插入 链表  
List.push_front(1); 

List.insert(迭代器变量类型的 位置 , x);
// 例如 在 k 前面 插入 x 
pos[x] = List.insert(pos[k],x);  
// 插入的同时 会 返回 插入位置的迭代器变量值   默认 插在 给定位置的前面
// 插入的 同时 标记x的位置变量 
// 例如 在 k 后面 插入 x 
auto iter = next(pos[k]); // 找到 k 的 后面元素的位置 
auto iter = prev(pos[k]); // 前面 
pos[x] = List.insert(iter,x);



List.splice(l,List,r);  1 2 3 4 -> 4 1 2 3   
    l = 1 的 迭代器 
    r = 4 的 迭代器
    连通 迭代器一起交换 

```

**删除**  

```c++
List.erase(pos[x]); 
// 若 x 在 链表中  则 删除 x 
```

[数组操作]([D-小红数组操作_牛客周赛 Round 31 (nowcoder.com)](https://ac.nowcoder.com/acm/contest/74362/D)) 

```c++
#include <iostream>
#include <list>
#include <unordered_map>
using namespace std;
const int N = 2e6 + 50;
using Iter = list <int> :: iterator ;
list <int> List;
unordered_map < int, Iter > pos; 
int main(){
    List.push_back(0);
    pos[0] = List.begin();
    int q,t,x,y;
    cin>>q;
    for(int i = 1; i <= q; i ++) {
        cin>>t;
        if(t == 1) {
            cin>>x>>y;
            auto iter = next(pos[y]);
            pos[x] = List.insert(iter,x);
        }
        else {
            cin>>x;
            List.erase(pos[x]);
        }
    }
    cout<< List.size() - 1 << endl;
    for(auto it : List) {
        if(it == 0) continue;
        cout<< it <<" ";
    }
    return 0;
}
```

**next_permutation**

```c++
std::string s;
std::cin >> s;

std::next_permutation(s.begin(),s.end());


	std::vector<int> v; // 1-8 全排列
	for(int i = 1; i < 9; i++ ) {
		v.push_back(i);
	}
	do {
		for(int i = 0; i < 7; i++) std::cout << v[i] << ' ';
		std::cout << v[7] << '\n';
	}while(std::next_permutation(v.begin(),v.end()));
```

**goto**

````c++
	for(auto [per,str] : mp) {
		for(auto s1 : str) {
			for(auto s2 : str) {
				if(s1 != s2) {
					if(check(s1,s2) == false) 
						goto next_pos; // 脱离循环 跳到该位置 
				}
			}
			f[per].insert(s1);
			next_pos:;
		}
	} 
````

### memcpy

```c++
int a[N],b[N];
std::memcpy(b,a,sizeof(a));
```

### starts_with  ends_with  c++ 20

```
int main() {
    std::string s = "bocchi the rock";
    std::cout << std::boolalpha ; // true 输出 true 而不是 1
    std::cout << s.starts_with("bocchi") << '\n';  // true
}

```

### Copy

```c++
#include <vector>
#include <algorithm>
#include <iterator>
 
int main() {
    std::vector<int> data = {1, 2, 3, 4, 5};
    std::vector<int> destination(data.size());
 
    // 使用std::copy来安全地复制数据
    std::copy(data.begin(), data.end(), destination.begin());
 
    // 使用std::copy_n来安全地复制指定数量的元素
    std::copy_n(data.begin(), 3, std::ostream_iterator<int>(std::cout, " "));
 
    // 使用std::transform来转换和复制元素
    std::transform(data.begin(), data.end(), destination.begin(), [](int x) { return x * 2; });
 
    // 使用std::back_inserter来将元素复制到一个动态数组中
    std::vector<int> dynamic_copy;
    std::copy(data.begin(), data.end(), std::back_inserter(dynamic_copy));
 
    return 0;
}
```

