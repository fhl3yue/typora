```
class STR {
public:
    std::string s;
    int len;

    STR(std::string st) {
        s = st; // 初始化成员变量 s
        len = st.length();
    }

    std::vector<int> strInt(const std::string &input) { // 提取字符串中所有数字
        std::vector<int> num;
        std::regex integerRegex("-?\\d+");
        std::sregex_iterator it(input.begin(), input.end(), integerRegex);
        std::sregex_iterator end;

        while (it != end) {
            num.push_back(std::stoi(it->str()));
            ++it;
        }
        return num;
    }

    bool issub(std::string o) { // 判定字串
        std::string::size_type idx = s.find(o);
        if (idx == std::string::npos) return false;
        else return true;
    }

    std::string str(int i, int j) {
        return s.substr(i, j);
    }

    int query(std::string a) { // 统计不重叠的子串数量
        int count = 0;
        std::string::size_type idx = s.find(a);
        while (idx != std::string::npos) {
            ++count;
            idx = s.find(a, idx + a.length());
        }
        return count;
    }

    std::pair<int, std::string> lowper(int id) {
        if (id == 1) { // 大写统计和转换
            int d = std::count_if(s.begin(), s.end(), ::isupper);
            std::string dx = s;
            std::transform(dx.begin(), dx.end(), dx.begin(), ::toupper); // 转换为大写
            return {d, dx};
        } else { // 小写统计和转换
            int x = std::count_if(s.begin(), s.end(), ::islower);
            std::string xx = s;
            std::transform(xx.begin(), xx.end(), xx.begin(), ::tolower); // 转换为小写
            return {x, xx};
        }
    }
};
```
### 查找某一个串是否是 s1 字串

```c++
	string s1;
	cin >> s1;
	string s2 = "it";
	string::size_type idx;
	idx = s1.find(s2);
	if(idx == string::npos ) cout << "NO" << endl;
	else cout << "YES" << endl;
```

### 最后出现的位置

```c++
int pos = s.rfind('#');
```

### 大小写字母

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

### 字符串裁剪

```c++
std::string sub = C.substr(i,j); // 从 i 开始，向后截取j个字符做串
```
### 任意字符集都可作为分隔符时的查询
```
while(1){
        size_t pos = s.find_first_of(".?!", st);
        if(pos == string::npos) break;
        string op = s.substr(st, pos - st);
        S.push_back(op);
        st = pos + 1;
    }
```
### string  查询字串数量

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


