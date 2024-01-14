# 静态区间第 k 小

## 代码

时间复杂度 $O(n \log W) - O(\log W)$。

空间复杂度 $O(n + m \log W)$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int MAXN = 2e5 + 5;
const int MAXM = 2e5 + 5;

int n, m;
int a[MAXN];

struct HJT {
    #define M ((L + R - 1) >> 1)
    #define lson(u) t[u].lson
    #define rson(u) t[u].rson
    struct Node {
        int lson, rson;
        int val;
    } t[MAXN * 32];
    int tot = 0;
    int rt[MAXM];
    void pushup(int u) {
        t[u].val = t[lson(u)].val + t[rson(u)].val;
    }
    void insert(int &u, int pre, int L, int R, int x, int k) {
        u = ++tot;
        lson(u) = lson(pre);
        rson(u) = rson(pre);
        t[u].val = t[pre].val;
        if (L == R) {
            t[u].val += k;
            return;
        }
        if (x <= M)
            insert(lson(u), lson(pre), L, M, x, k);
        else
            insert(rson(u), rson(pre), M+1, R, x, k);
        pushup(u);
    }
    int query(int u, int v, int L, int R, int k) {
        if (L == R)
            return L;
        int tmp = t[lson(u)].val - t[lson(v)].val;
        if (k <= tmp)
            return query(lson(u), lson(v), L, M, k);
        return query(rson(u), rson(v), M+1, R, k - tmp);
    }
};

HJT tr;

int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> n >> m;
    tr.rt[0] = ++tr.tot;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        tr.insert(tr.rt[i], tr.rt[i-1], -1e9, 1e9, a[i], 1);
    }

    while (m--) {
        int l, r, k; cin >> l >> r >> k;
        cout << tr.query(tr.rt[r], tr.rt[l-1], -1e9, 1e9, k) << '\n';
    }
    return 0;
}
```

## 模板题目

[P3834 【模板】可持久化线段树 2](https://www.luogu.com.cn/problem/P3834)