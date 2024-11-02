# KMP 自动机

## 代码

```cpp
    for (int i = 2, p = 0; i <= m; i++) {
        while (p != 0 && T[p+1] != T[i])
            p = nxt[p];
        p += (T[p+1] == T[i]);
        nxt[i] = p;
    }
```

```cpp
    for (int i = 1, p = 0; i <= n; i++) {
        while (p != 0 && T[p+1] != S[i])
            p = nxt[p];
        p += (T[p+1] == S[i]);
        if (p == m)
            cout << i-m+1 << '\n', p = nxt[p];
    }
```

```cpp
    for (int i = 0; i <= m; i++)
        for (int c = 0; c <= 9; c++) // 枚举字符集
            if (c == T[i+1])
                dt[i][c] = i + 1;
            else
                dt[i][c] = dt[nxt[i]][c];
```

## 注

第一段代码构建 $T$ 的 nxt 数组。

第二段代码输出 $S$ 中所有出现 $T$ 的位置。

第三段代码根据 nxt 数组构建 $T$ 的 KMP 自动机。

## 模板题目

[P3375 【模板】KMP](https://www.luogu.com.cn/problem/P3375)