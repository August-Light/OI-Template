# exBSGS

## 代码

时间复杂度 $\Theta(\sqrt M)$。

```cpp
ll q[MAXN], r[MAXN];
ll exBSGS(ll a, ll b) {
    umap<ll, ll> mp[2];
    ll t = sqrt(MOD * 2) + 1;
    r[0] = 1; for (int i = 1; i <= t; i++) r[i] = r[i-1] * a % MOD;
    q[0] = 1; for (int i = 1; i <= t; i++) q[i] = q[i-1] * r[t] % MOD;
    for (ll i = 1; i <= t; i++) {
        ll cur = q[i];
        if (mp[0].find(cur) == mp[0].end())
            mp[0][cur] = i;
        else if (mp[1].find(cur) == mp[1].end())
            mp[1][cur] = i;
    }
    ll ans = INF;
    for (ll i = 1; i <= t; i++) {
        ll cur = r[i] * b % MOD;
        if (mp[0].find(cur) != mp[0].end())
            if (q[mp[0][cur]-1] * r[t-i] % MOD == b)
                ans = min(ans, mp[0][cur] * t - i);
        if (mp[1].find(cur) != mp[1].end())
            if (q[mp[1][cur]-1] * r[t-i] % MOD == b)
                ans = min(ans, mp[1][cur] * t - i);
    }
    if (ans != INF)
        return ans;
    return -1; // No Solution
}
```

## 模板题目

[P4195 【模板】扩展 BSGS/exBSGS](https://www.luogu.com.cn/problem/P4195)