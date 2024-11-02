# Miller-Rabin

## 代码

时间复杂度 $O(k \log^2 n)$。$k$ 为检验次数。代码中为 $12$。

//TODO: 事实上复杂度可以优化到 $O(k \log n)$。

```cpp
ll qpow(i128 a, ll b, ll MOD) {
    i128 ret = 1;
    while (b) {
        if (b & 1)
            (ret *= a) %= MOD;
        (a *= a) %= MOD;
        b >>= 1;
    }
    return ret;
}

bool MillerRabinPass(ll a, ll p) {
    ll d = p-1, x;
    while (d % 2 == 0) {
        d /= 2;
        x = qpow(a, d, p);
        if (x == p-1)
            return true;
        if (x != 1)
            return false;
    }
    return true;
}
const ll bases[] = {2,3,5,7,11,13,17,19,23,29,31,37};
bool is_prime(ll p) {
    if (p == 2)
        return true;
    if (p == 1 || p % 2 == 0)
        return false;
    for (int t = 0; t < 12 && bases[t] < p; t++)
        if (!MillerRabinPass(bases[t], p))
            return false;
    return true;
}
```

## 注

底数选择：（来源：[题解 P4718/论 Miller-Rabin 算法的确定性化](https://www.luogu.com.cn/blog/wangrx/miller-rabin)）

- 对 $2^{32}$ 范围内的数判素，可以使用：`{2,7,61}`。

- 对 $2^{64}$ 范围内的数判素，可以使用：`{2,325,9375,28178,450775,9780504,1795265022}`。

- 在考场上对 $2^{64}$ 范围内的数判素，也可以使用前 $12$ 个素数：`{2,3,5,7,11,13,17,19,23,29,31,37}`。
- 在考场上对 $10^{24}$ 范围内的数判素，可以使用前 $13$ 个素数：`{2,3,5,7,11,13,17,19,23,29,31,37,41}`。

## 模板题目

[U287941 【模板】Miller-Rabin](https://www.luogu.com.cn/problem/U287941)

## debug

特判 $2$。

`qpow` 要开 `__int128`。

先 `d /= 2` 再 `qpow(a, d, p)`。