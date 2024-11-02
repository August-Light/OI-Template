# SA

## 代码

```cpp
int sa[MAXN], rk[MAXN * 2], tmp[MAXN * 2];
void build_SA(string S) {
    rep(i, 1, n)
        sa[i] = i, rk[i] = S[i];
    for (int w = 1; w <= n; w <<= 1) {
        auto cmp = [&](int x, int y) -> bool {
            if (rk[x] == rk[y])
                return rk[x+w] < rk[y+w];
            return rk[x] < rk[y];
        };
        sort(sa+1, sa+n+1, cmp);
        rep(i, 1, n)
            tmp[sa[i]] = tmp[sa[i-1]] + cmp(sa[i-1], sa[i]);
        copy(tmp+1, tmp+n+1, rk+1);
    }
}
```

## 注

求 height 数组：

```cpp
    int k = 0;
    rep(i, 1, n) {
        int j = sa[rk[i] - 1];
        if (k) k--;
        while (S[i + k] == S[j + k])
            k++;
        h[rk[i]] = k;
    }
```

## 模板题目

[P3809 【模板】后缀排序](https://www.luogu.com.cn/problem/P3809)