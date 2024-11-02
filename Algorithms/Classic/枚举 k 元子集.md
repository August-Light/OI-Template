# 枚举 k 元子集

## 代码

时间复杂度 $\Theta(n \binom n k)$。

```cpp
    rep(i, 1, k)
        a[i] = true;
    do {
        rep(i, 1, n)
            if (a[i]) {
                // do something
            }
        cout << '\n';
    } while (prev_permutation(a+1, a+n+1));
```

## 注

Gosper's Hack 可以做到 $\Theta(k \binom n k)$，但一般不实用。

## 模板题目

[P1157 组合的输出](https://www.luogu.com.cn/problem/P1157)