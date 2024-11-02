# [国家集训队] Crash的数字表格

## 代码

时间复杂度 $\Theta(n) - O(n^{\frac 3 4})$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int MAXN = 1e7 + 5;
const ll MOD = 20101009;
const ll inv2 = 10050505;

bool vis[MAXN];
vector<ll> primes;
ll mu[MAXN];
ll sum[MAXN];

void init(ll n) {
    vis[1] = 1;
    mu[1] = 1;
    for (ll i = 2; i <= n; i++) {
        if (!vis[i]) {
            primes.push_back(i);
            mu[i] = -1;
        }
        for (auto j : primes) {
            ll k = i * j; if (k > n) break;
            vis[k] = 1;
            if (i % j == 0) {
                mu[k] = 0;
                break;
            }
            mu[k] = -mu[i];
        }
    }
    for (ll i = 1; i <= n; i++) {
        ll tmp = i * i % MOD * mu[i] % MOD;
        sum[i] = (sum[i-1] + tmp) % MOD;
    }
}

ll n, m;

ll s(ll x) {
    return x * (x + 1) % MOD * inv2 % MOD;
}
ll g(ll n, ll m) {
    ll ret = 0;
    for (ll l = 1, r; l <= n; l = r + 1) {
        ll v1 = n / l, v2 = m / l;
        r = min(n / v1, m / v2);
        (ret += (sum[r] - sum[l-1] + MOD) % MOD * s(v1) % MOD * s(v2) % MOD) %= MOD;
    }
    return ret;
}
ll f(ll n, ll m) {
    ll ans = 0;
    for (ll l = 1, r; l <= n; l = r + 1) {
        ll v1 = n / l, v2 = m / l;
        r = min(n / v1, m / v2);
        (ans += g(v1, v2) * (s(r) - s(l-1) + MOD) % MOD) %= MOD;
    }
    return ans;
}

int main() {
    cin >> n >> m;
    if (n > m) swap(n, m);
    init(n);
    cout << f(n, m) << '\n';
    return 0;
}
```

## 模板题目

[P1829 [国家集训队] Crash的数字表格 / JZPTAB](https://www.luogu.com.cn/problem/P1829)