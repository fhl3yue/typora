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

