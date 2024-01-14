# 静态区间 mex

## 代码

时间复杂度 $O(n \log W) - O(\log W)$。

空间复杂度 $O(n + m \log W)$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int MAXN = 2e5 + 5;

int n, m;
int a[MAXN];

struct HJT {
    #define M ((L + R) >> 1)
    #define lson(u) (t[u].lson)
    #define rson(u) (t[u].rson)
    struct Node {
        int lson, rson;
        ll val;
    } t[MAXN * 19];
    int tot = 0;
    int rt[MAXN];
    void pushup(int u) {
        t[u].val = min(t[lson(u)].val, t[rson(u)].val);
    }
    void insert(int &u, int pre, int L, int R, int x, ll v) {
        u = ++tot;
        lson(u) = lson(pre);
        rson(u) = rson(pre);
        t[u].val = t[pre].val;
        if (L == R) {
            t[u].val = v;
            return;
        }
        if (x <= M)
            insert(lson(u), lson(pre), L, M, x, v);
        else
            insert(rson(u), rson(pre), M+1, R, x, v);
        pushup(u);
    }
    ll query(int u, int L, int R, int x) {
        if (L == R)
            return L;
        if (t[lson(u)].val < x)
            return query(lson(u), L, M, x);
        return query(rson(u), M+1, R, x);
    }
};

HJT tr;

int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> n >> m;
    tr.rt[0] = ++tr.tot;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        tr.insert(tr.rt[i], tr.rt[i-1], 0, n, a[i], i);
    }
    while (m--) {
        int l, r; cin >> l >> r;
        cout << tr.query(tr.rt[r], 0, n, l) << '\n';
    }
    return 0;
}
```

## 模板题目

[P4137 Rmq Problem / mex](https://www.luogu.com.cn/problem/P4137)