# GCD 卷积与 LCM 卷积

## 代码

时间复杂度 $\Theta(n \log \log n)$。

空间复杂度 $\Theta(n)$。

```cpp
int n;
ll f[MAXN], g[MAXN];
ll h[MAXN];
void gcd_convolution() {
    for (auto j : primes)
        for (int i = n / j; i >= 1; i--)
            (f[i] += f[i * j]) %= MOD;
    for (auto j : primes)
        for (int i = n / j; i >= 1; i--)
            (g[i] += g[i * j]) %= MOD;
    rep(i, 1, n)
        h[i] = f[i] * g[i] % MOD;
    for (auto j : primes)
        for (int i = 1; i * j <= n; i++)
            (h[i] -= h[i * j]) %= MOD;
    rep(i, 1, n)
        (h[i] += MOD) %= MOD;
}
```

```cpp
int n;
ll f[MAXN], g[MAXN];
ll h[MAXN];
void lcm_convolution() {
    for (auto j : primes)
        for (int i = 1; i * j <= n; i++)
            (f[i * j] += f[i]) %= MOD;
    for (auto j : primes)
        for (int i = 1; i * j <= n; i++)
            (g[i * j] += g[i]) %= MOD;
    rep(i, 1, n)
        h[i] = f[i] * g[i] % MOD;
    for (auto j : primes)
        for (int i = n / j; i >= 1; i--)
            (h[i * j] -= h[i]) %= MOD;
    rep(i, 1, n)
        (h[i] += MOD) %= MOD;
}
```

## 模板题目

[Gcd Convolution](https://judge.yosupo.jp/problem/gcd_convolution) & [Lcm Convolution](https://judge.yosupo.jp/problem/lcm_convolution)