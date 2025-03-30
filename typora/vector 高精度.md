**高精度 + 高精度**

```c++
vector<int> add(vector<int> a, vector<int> b){
    if(a.size() < b.size()) return add(b, a);
    vector<int> temp;
    int cur = 0;    
    reverse(a.begin(),a.end());
    reverse(b.begin(),b.end());
    for(int i = 0; i < a.size(); i++){
        if(i < b.size()) cur += b[i];
        cur += a[i];
        temp.push_back(cur % 10);
        cur /= 10;
    }
    if(cur) temp.push_back(cur);
    while(temp.size() > 1 && temp.back() == 0) temp.pop_back();
    reverse(temp.begin(), temp.end());
    return temp;
}
```



**高精度 * 低精度**

```c++
vector<int> mul(vector<int> a, int b){// 正向大数 a 
    reverse(a.begin(), a.end()); 
    vector<int> res; 
    int temp = 0; 
    int len = a.size();
    for(int i = 0; i < len || temp; i++){
        if(i < len) temp = temp + a[i] * b; 
        res.push_back(temp % 10); 
        temp /= 10;
    }
    while(res.size() > 1 && res.back() == 0) res.pop_back();
    reverse(res.begin(), res.end()); 
    return res;
}

```

**高精度 / 低精度**

```c++

vector<int> div(vector<int> a, int b, int& r){ // 正向大数 a
    vector<int> temp;
    int len = a.size();
    for(int i = 0; i < len; i++){
        r = a[i] + r * 10; 
        temp.push_back(r / b); 
        r %= b; 
    }
    reverse(temp.begin(), temp.end()); 
    while(temp.size() > 1 && temp.back() == 0) temp.pop_back();
    reverse(temp.begin(), temp.end()); 
    return temp;
}
```

**高精度/高精度**
```
vector<int> div(vector<int> a, vector<int> b, vector<int>& r) {
    vector<int> temp; // 存储商
    r.clear();            // 初始化余数为空

    // 如果被除数小于除数，商为0，余数为被除数
    if (a.size() < b.size() || (a.size() == b.size() && a < b)) {
        r = a;
        return {0};
    }

    r = {}; // 当前余数
    for (int i = 0; i < a.size(); ++i) {
        r.push_back(a[i]); // 当前位加入余数
        while (r.size() > 1 && r[0] == 0) r.erase(r.begin()); // 去掉前导零

        // 当前余数和除数比较，判断能取多少倍
        int count = 0;
        while (r.size() > b.size() || (r.size() == b.size() && r >= b)) {
            // 执行余数减去除数
            for (int j = r.size() - 1, k = b.size() - 1; k >= 0; --j, --k) {
                r[j] -= b[k];
                if (r[j] < 0) {
                    r[j] += 10;
                    r[j - 1]--;
                }
            }
            while (r.size() > 1 && r[0] == 0) r.erase(r.begin()); // 去掉前导零
            count++;
        }
        temp.push_back(count); // 记录当前商
    }

    // 去掉商的前导零
    while (temp.size() > 1 && temp[0] == 0) temp.erase(temp.begin());

    return temp;
}
```
$O(n*m)$   
[1/40 高精度小数运算](https://ac.nowcoder.com/acm/contest/98985/C)