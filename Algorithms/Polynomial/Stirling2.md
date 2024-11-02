# Stirling2

## 代码

递推公式：时间复杂度 $\Theta(n^2)$。

```cpp
    S[0][0] = S[1][1] = 1;
    for (ll i = 2; i <= n; i++)
        for (ll j = 1; j <= i; j++)
            (S[i][j] = S[i-1][j-1] + j * S[i-1][j]) %= MOD;
```

第二类斯特林数·行：时间复杂度 $\Theta(n \log n)$。

```cpp
    rep(i, 0, n) {
        a[i] = qpow(i, n) * ifac[i] % MOD;
        b[i] = ((i % 2 ? -1 : 1) * ifac[i] % MOD + MOD) % MOD;
    }
    NTT(a, tot), NTT(b, tot);
    for (int i = 0; i < tot; i++)
        c[i] = a[i] * b[i] % MOD;
    INTT(c, tot);
    rep(i, 0, n)
        cout << c[i] << " \n"[i == n];
```

## 模板题目

[P5395 第二类斯特林数·行](https://www.luogu.com.cn/problem/P5395)

## debug

容斥时有负数，要加一个模数变回来。

在 $[n+1, tot]$ 区间内，$c$ 的值不一定是 $0$，可能需要清空。