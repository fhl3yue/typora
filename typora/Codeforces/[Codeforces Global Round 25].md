[Codeforces Global Round 25](https://codeforces.com/contest/1951)

**A**: 

1的数量为 num 

num 为偶数  （ > 2 )  YES  奇数 ： NO  

num == 2 特判是否相邻   相邻 NO   不相邻 YES  

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
const int P = 1e8;
typedef long long ll;
const int M = 2007;	
int n;
struct point{
	double x;
	double y;
}t[N];
double dis(point a,point b) {
	return sqrt( (a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y));
}
void solve() {
	cin >> n;
	string s;
	cin >> s;
	vector<int> f(3);
	for(int i = 0; i < n ; i++) 
	{
		int x  = s[i] - '0';
		f[x]++;
	}
	if(f[1] & 1) {
		cout << "NO" << endl;
	}
	else {
		if(f[1] == 2) {
			bool flag = false;
			for(int i = 0; i < n - 1; i ++) {
				int x = s[i] - '0';
				int y = s[i+1] - '0';
				if(x == 1 && y == 1) {
					flag = true;
				}
			}
			if(flag == false) cout << "YES" << endl;
			else cout << "NO" << endl;
		}
		else cout << "YES" << endl;
	}
	return;
}
int main() {
	int _ = 1;
	cin >> _ ;
	while(_ --) {
		solve();
	}
	return 0;
}
```



**B**：  

x = a[k]

在 第 K 之前 有 比它大的 交换  

或直接 与第一个交换  （losed)

两者取最大值    为答案 

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
const int P = 1e8;
typedef long long ll;
const int M = 2007;	
int n,k;
void solve() {
	cin >> n >> k;
	bool flag = false;
	vector<int> a( n + 1);
	for(int i = 1; i <= n; i++) cin >> a[i];
	int x = a[k],pos = 0;
	for(int i = 1; i < k; i ++) {
		if(a[i] > x) {
			swap(a[i],a[k]);
			flag = true;
			pos = i;
			break;
		}
	}
	/*for(int i = 1; i <= n; i++) {
		cout << a[i] << " ";
	} cout << endl;*/
	int y = a[1];
	int cnt = 0;
	for(int i = 2; i <= n; i++) {
		y = max(y,a[i]);
		if(y == x) cnt++;
	}
	int tot = 0;
	if(flag == true) swap(a[pos],a[k]);  swap(a[1],a[k]); 
	int z = a[1];
	for(int i = 2; i <= n; i++) {
		z = max(z,a[i]);
		if(z == x) tot++;
	}
	cout << max(cnt,tot) << endl;
	return;
}// 7 2 727 10 12 13
// 7 2 12 10 727 13
int main() {
	int _ = 1;
	cin >> _ ;
	while(_ --) {
		solve();
	}
	return 0;
}
```

**C**: 

