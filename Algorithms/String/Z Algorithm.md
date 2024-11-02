# Z Algorithm

## 代码

```cpp
    z[1] = m;
    int l = 0, r = 0;
    rep(i, 2, m) {
        if (i <= r)
            z[i] = min(z[i - l + 1], r - i + 1);
        while (i + z[i] <= m && T[i + z[i]] == T[z[i] + 1])
            z[i]++;
        if (i + z[i] - 1 > r)
            r = i + z[i] - 1, l = i;
    }

    l = 0, r = 0;
    rep(i, 1, n) {
        if (i <= r)
            p[i] = min(z[i - l + 1], r - i + 1);
        while (i + p[i] <= n && S[i + p[i]] == T[p[i] + 1])
            p[i]++;
        if (i + p[i] - 1 > r)
            r = i + p[i] - 1, l = i;
    }
```

## 模板题目

[P5410 【模板】扩展 KMP/exKMP（Z 函数）](https://www.luogu.com.cn/problem/P5410)