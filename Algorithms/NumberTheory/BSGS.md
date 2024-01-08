# BSGS

## 代码

时间复杂度 $\Theta(\sqrt M)$。

```cpp
ll BSGS(ll a, ll b) {
    umap<ll, ll> mp;
    ll t = sqrt(MOD) + 1;
    ll cur = 1;
    for (ll i = 1; i <= t; i++) {
        (cur *= a) %= MOD;
        mp[b * cur % MOD] = i;
    }
    ll cur2 = cur;
    for (ll i = 1; i <= t; i++) {
        if (mp.find(cur2) != mp.end())
            return i * t - mp[cur2];
        (cur2 *= cur) %= MOD;
    }
    return -1; // No Solution
}
```

## 模板题目

[P3846 [TJOI2007] 可爱的质数/【模板】BSGS](https://www.luogu.com.cn/problem/P3846)