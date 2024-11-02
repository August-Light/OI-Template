# FWT

## 代码

时间复杂度 $\Theta(n \log n)$。（$n$ 为序列长度）

时间复杂度 $\Theta(n 2^n)$。（$2^n$ 为序列长度）

```cpp
#include <bits/stdc++.h>
#define rep(i, l, r) for (int i = (l); i <= (r); i++)
#define per(i, r, l) for (int i = (r); i >= (l); i--)
using namespace std;
typedef long long ll;

typedef modint998244353 mint;

const int MAXN = (1 << 20) + 5;

int n, tot;
mint a[MAXN], b[MAXN], c[MAXN];
mint A[MAXN], B[MAXN], C[MAXN];

void FWT_or(mint a[]) {
    rep(i, 0, n)
        rep(u, 0, tot)
            if (u >> i & 1)
                a[u] += a[u ^ (1 << i)];
}
void invFWT_or(mint a[]) {
    rep(i, 0, n)
        rep(u, 0, tot)
            if (u >> i & 1)
                a[u] -= a[u ^ (1 << i)];
}

void FWT_xor(mint a[]) {
    for (int len = 1; len <= tot; len <<= 1)
        for (int p = 0; p <= tot; p += (len << 1))
            for (int i = p; i < p+len; i++) {
                auto x = a[i], y = a[i + len];
                a[i] = x + y;
                a[i+len] = x - y;
            }
}
void invFWT_xor(mint a[]) {
    FWT_xor(a);
    rep(i, 0, tot)
        a[i] /= (1 << n);
}

int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> n; tot = (1 << n) - 1;
    rep(i, 0, tot)
        cin >> a[i];
    rep(i, 0, tot)
        cin >> b[i];

    // or 卷积
    rep(i, 0, tot) A[i] = a[i], B[i] = b[i];
    FWT_or(A), FWT_or(B);
    rep(i, 0, tot) C[i] = A[i] * B[i];
    invFWT_or(C);
    rep(i, 0, tot) c[i] = C[i];
    rep(i, 0, tot) cout << c[i] << " \n"[i == tot];

    // and 卷积
    rep(i, 0, tot) A[i] = a[i ^ tot], B[i] = b[i ^ tot];
    FWT_or(A), FWT_or(B);
    rep(i, 0, tot) C[i] = A[i] * B[i];
    invFWT_or(C);
    rep(i, 0, tot) c[i] = C[i ^ tot];
    rep(i, 0, tot) cout << c[i] << " \n"[i == tot];

    // xor 卷积
    rep(i, 0, tot) A[i] = a[i], B[i] = b[i];
    FWT_xor(A), FWT_xor(B);
    rep(i, 0, tot) C[i] = A[i] * B[i];
    invFWT_xor(C);
    rep(i, 0, tot) c[i] = C[i];
    rep(i, 0, tot) cout << c[i] << " \n"[i == tot];
    return 0;
}
```

## 模板题目

[P4717 【模板】快速莫比乌斯/沃尔什变换 (FMT/FWT)](https://www.luogu.com.cn/problem/P4717)