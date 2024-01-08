# 炸脖龙 I

## 代码

时间复杂度：

- 预处理 $O(p + n)$。
- 单次修改 $O(\log n)$。
- 单次查询 $O(\log n \log p)$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef __int128 i128;

const int MAXN = 5e5 + 5;
const int MAXW = 2e7 + 5;

vector<int> primes;
bool vis[MAXW];
int phi[MAXW];
void init(int n) {
    vis[1] = 1;
    phi[1] = 1;
    for (int i = 2; i <= n; i++) {
        if (!vis[i])
            primes.push_back(i), phi[i] = i - 1;
        for (auto j : primes) {
            int k = i * j;
            if (k <= n) {
                vis[k] = 1;
                if (i % j == 0) {
                    phi[k] = phi[i] * j;
                    break;
                }
                phi[k] = phi[i] * phi[j];
            } else break;
        }
    }
}

i128 qpow(i128 a, i128 b, i128 p) {
    i128 ret = 1;
    while (b) {
        if (b & 1) {
            ret *= a; if (ret >= p) ret = ret % p + p;
        }
        a *= a; if (a >= p) a = a % p + p;
        b >>= 1;
    }
    return ret;
}

int n, m;
ll a[MAXN];

int lowbit(int x) {
    return x & -x;
}
struct Fenwick {
    ll c[MAXN];
    ll query(int x) {
        ll ret = 0;
        for (int i = x; i; i -= lowbit(i))
            ret += c[i];
        return ret;
    }
    void add(int x, ll k) {
        for (int i = x; i <= n; i += lowbit(i))
            c[i] += k;
    }
};
Fenwick tr;

ll f(int l, int r, ll p) {
    if (l == r+1 || p == 1)
        return 1;
    return qpow(tr.query(l), f(l+1, r, phi[p]), p);
}

int main() { ios::sync_with_stdio(0); cin.tie(0);
    init(2e7);
    cin >> n >> m;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        tr.add(i, a[i] - a[i-1]);
    }
    while (m--) {
        int op; cin >> op;
        if (op == 1) {
            int l, r, k; cin >> l >> r >> k;
            tr.add(l, k); tr.add(r+1, -k);
        } else if (op == 2) {
            int l, r, p; cin >> l >> r >> p;
            cout << f(l, r, p) % p << '\n';
        }
    }
    return 0;
}

```

## 注

这份代码中使用的是 $O(n \log n)$ 建树状数组。**时间复杂度有所不同**。

这份代码中的 `qpow` 不是普通的快速幂，而是为了扩展欧拉定理而服务的。它在快速幂的同时保住 $a^b$ 和 $p$ 的大小关系。

## 模板题目

[P3934 [Ynoi2016] 炸脖龙 I](https://www.luogu.com.cn/problem/P3934)

## debug

- 扩展欧拉定理的复杂分类讨论。务必注意是混循环。可以参照代码中的 `qpow` 函数。
- 因为不同于以往的 `qpow` 实现，调用 `f(l, r, p)` 查询后要 `% p`。