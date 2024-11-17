**查找某一个串是否是 s1 字串**

```c++
	string s1;
	cin >> s1;
	string s2 = "it";
	string::size_type idx;
	idx = s1.find(s2);
	if(idx == string::npos ) cout << "NO" << endl;
	else cout << "YES" << endl;
```

**最后出现的位置** 

```c++
int pos = s.rfind('#');
```

**大小写字母**

```c++
    std::string S;
    std::cin >> S;
    int c = std::count_if(S.begin(),S.end(),::islower);  // 小写字母数量
    int d = std::count_if(S.begin(),S.end(),::isupper);  // 大写字母数量
    if(c < d) std::transform(S.begin(),S.end(),S.begin(),::toupper); // 修改为 大写
    else std::transform(S.begin(),S.end(),S.begin(),::tolower); 
	// 起始范围  终止范围  开始修改的位置 
    std::cout << S << '\n';
```

**字符串裁剪**

```c++
std::string sub = C.substr(i,j); // 从 i -> j w
```

**string  查询字串数量**

```c++
	auto query = [&] (std::string A, std::string a) -> int { // aaa -> aa = 1
    	int count = 0;  
    	std::string::size_type idx;
		idx = A.find(a);
    	while (idx != std::string::npos) {  
        	++count;  
        	idx = A.find(a, idx + a.length());  
    	}
    	return count;
	};
```

