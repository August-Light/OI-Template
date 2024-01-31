# 莫队

## 代码

时间复杂度 $O(n \sqrt m)$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int MAXN = 5e4 + 5;
const int MAXM = 5e4 + 5;
const int MAXW = 5e4 + 5;

int n, m, k;
int a[MAXN], c[MAXW];

int pos[MAXN]; // pos[x] 为下标 x 的所在块
struct Q {
    int l, r, id;
} q[MAXM];
ll res = 0, ans[MAXM];

ll sq(int x) {
    return (ll)x*x;
}
void add(int x) {
    res -= sq(c[a[x]]);
    res += sq(++c[a[x]]);
}
void del(int x) {
    res -= sq(c[a[x]]);
    res += sq(--c[a[x]]);
}

int main() {
    cin >> n >> m >> k;
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    for (int i = 1; i <= m; i++)
        cin >> q[i].l >> q[i].r, q[i].id = i;

    int block_size = sqrt(n);
    for (int i = 1; i <= n; i++)
        pos[i] = i / block_size;
    sort(q + 1, q + m + 1, [](Q x, Q y) {
        if (pos[x.l] == pos[y.l])
            return x.r < y.r;
        return pos[x.l] < pos[y.l];
    });
    int l = 1, r = 0;
    for (int i = 1; i <= m; i++) {
        while (l > q[i].l) add(--l);
        while (r < q[i].r) add(++r);
        while (l < q[i].l) del(l++);
        while (r > q[i].r) del(r--);
        ans[q[i].id] = res;
    }

    for (int i = 1; i <= m; i++)
        cout << ans[i] << '\n';
    return 0;
}
```

## 模板题目

[P2709 小B的询问](https://www.luogu.com.cn/problem/P2709)