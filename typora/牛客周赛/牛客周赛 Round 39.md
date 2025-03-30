牛客周赛 Round 39

**F**:   01串 A，B  每次选择某个串 的一个区间 [l,r] 全部 变成1  

求 两个字符串 有多少个位置的值都是 1   

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 2e6 + 50;
const int P = 1e8;
typedef long long ll;
const int M = 2007;	
int n,m,k;
int a[N],b[N];
struct node{
	int l,r,c1,c2,c;
	// c1: A [l,r] 1 的 个数
	// c2: B [l,r] 1 的 个数
	// c:  Ai & Bi 的串 [l,r] 的 1 的 个数 
	int lz1,lz2;// 懒标记 A  B
}tr[4040404];
void push_up(int u) { // 用儿子更新父亲
	tr[u].c = tr[u << 1].c + tr[u << 1 | 1].c;
	tr[u].c1 = tr[u << 1].c1 + tr[u << 1 | 1].c1;
	tr[u].c2 = tr[u << 1].c2 + tr[u << 1 | 1].c2;
	return; 
}
void build(int u,int l,int r) {
    if(l == r) {
	    tr[u] = {l,r,a[l],b[l],a[l] & b[l]};
        return;
	}
	else{
		tr[u] = {l,r,0,0,0};
		int mid = (l + r) >> 1;
		build(u << 1,l,mid);
		build(u << 1 | 1,mid + 1,r);
		push_up(u);
		return;
	}
}
void push_down(int u) { // 父亲更新儿子
    if(tr[u].lz1 ) {
		tr[u << 1].c1 = (tr[u << 1].r - tr[u << 1].l + 1);
		tr[u << 1].c = tr[u << 1].c2;
		tr[u << 1 | 1].c1 = (tr[u << 1 | 1].r - tr[u << 1 | 1].l + 1);
		tr[u << 1 | 1].c = tr[u << 1 | 1].c2;
		tr[u << 1].lz1 = 1;
		tr[u << 1 | 1].lz1 = 1;
		tr[u].lz1 = 0;
	}
	if(tr[u].lz2) {
		tr[u << 1].c2 = (tr[u << 1].r - tr[u << 1].l + 1);	
		tr[u << 1].c = tr[u << 1].c1;
		tr[u << 1 | 1].c2 = (tr[u << 1 | 1].r - tr[u << 1 | 1].l + 1);
		tr[u << 1 | 1].c = tr[u << 1 | 1].c1;
		tr[u << 1].lz2 = 1;
		tr[u << 1 | 1].lz2 = 1;
		tr[u].lz2 = 0;
	}
}
void modify(int u,int l,int r,int op) { // 区间修改
	if(l <= tr[u].l && tr[u].r <= r){
		if(op == 1) {
			tr[u].c1 = (tr[u].r - tr[u].l + 1);
			tr[u].c = tr[u].c2;
			tr[u].lz1 = 1;
		}
		else{
			tr[u].c2 = (tr[u].r - tr[u].l + 1);
			tr[u].c = tr[u].c1;
			tr[u].lz2 = 1;
		}
		return;
	}
	push_down(u);
	int mid = (tr[u].l + tr[u].r) >> 1;
	if(l <= mid) modify(u << 1,l,r,op);
	if(r > mid) modify(u << 1 | 1,l,r,op);
	push_up(u);
}
void solve() {
	cin >> n;
	string A,B;
	cin >> A >> B;
	for(int i = 0;i < n;i ++) {
		a[i + 1] = A[i] - '0';
		b[i + 1] = B[i] - '0';
	}
	build(1,1,n);// u l r
	cin >> m;
	char p;
	for(int i = 0,l,r;i < m;i ++) {
		cin >> p;
		int op = (p - 'A' + 1);
		cin >> l >> r;
		modify(1,l,r,op);
		cout << tr[1].c << endl;
	}
 	return;
}
int main() {
	int _ = 1;
	//cin >> _ ;
	while(_ --) {
		solve();
	}
	return 0;
}
```

