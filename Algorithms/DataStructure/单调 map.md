# 单调 map

## 代码

时间复杂度单次操作均摊 $O(\log n)$。

空间复杂度 $\Theta(n)$。

```cpp
struct MonotonicMap {
    map<ll, ll> mp;
    MonotonicMap() { mp[0] = 0; }
    ll query(ll x) {
        return prev(mp.upper_bound(x))->second;
    }
    void add(ll x, ll k) {
        if (query(x) >= k)
            return;
        mp[x] = k;
        auto it = next(mp.find(x));
        while (it != mp.end()) {
            auto lst = it++;
            if (lst->second <= k)
                mp.erase(lst);
            else
                break;
        }
    }
};
```

## 注

这份代码支持 **前缀最值** 和 **单点变大**。

## 模板题目

[P4954 [USACO09OPEN] Tower of Hay G](https://www.luogu.com.cn/problem/P4954)