# KMP 字符串匹配

## 代码

```cpp
    cin >> S >> T;
    n = S.length(), m = T.length();
    S.insert(0, "#"), T.insert(0, "#");

    rep(i, 2, m) {
        int p = nxt[i-1];
        while (p && T[p+1] != T[i])
            p = nxt[p];
        if (T[p+1] == T[i])
            nxt[i] = p+1;
    }

    int p = 0;
    rep(i, 1, n) {
        while (p && T[p+1] != S[i])
            p = nxt[p];
        if (T[p+1] == S[i])
            p++;
        if (p == m) {
            // match
        }
    }
```

## 模板题目

[P3375 【模板】KMP](https://www.luogu.com.cn/problem/P3375)