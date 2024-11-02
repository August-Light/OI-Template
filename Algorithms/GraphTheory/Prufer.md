# Prufer

## 代码

时间复杂度 $\Theta(n)$。

```cpp
int deg[MAXN];
void fa_to_prufer() {
    for (int u = 1; u <= n-1; u++)
        deg[fa[u]]++;
    int ptr = 1;
    for (int i = 1; i <= n-2; i++) {
        while (deg[ptr])
            ptr++;
        prufer[i] = fa[ptr];
        while (i <= n-2 && --deg[prufer[i]] == 0 && prufer[i] < ptr)
            prufer[i+1] = fa[prufer[i]], i++;
        ptr++;
    }
}
void prufer_to_fa() {
    for (int i = 1; i <= n-1; i++)
        deg[prufer[i]]++;
    prufer[n-1] = n;
    int ptr = 1;
    for (int i = 1; i <= n-1; i++) {
        while (deg[ptr])
            ptr++;
        fa[ptr] = prufer[i];
        while (i <= n-1 && --deg[prufer[i]] == 0 && prufer[i] < ptr)
            fa[prufer[i]] = prufer[i+1], i++;
        ptr++;
    }
}
```

## 模板题目

[P6086 【模板】Prufer 序列](https://www.luogu.com.cn/problem/P6086)