# 01 Trie

## 代码

时间复杂度 $O(\log W)$（单次操作）。

```cpp
struct Trie {
    int tot;
    int tr[MAXN * 30][2];
    Trie() {
        tot = 0;
        memset(tr, 0, sizeof tr);
    }
    int query_min(int x) {
        int u = 0, ret = 0;
        for (int i = (1 << 29); i; i >>= 1) {
            bool c = x & i;
            if (tr[u][c])
                u = tr[u][c];
            else {
                u = tr[u][!c];
                ret += i;
            }
        }
        return ret;
    }
    void insert(int x) {
        int u = 0;
        for (int i = (1 << 29); i; i >>= 1) {
            bool c = x & i;
            if (!tr[u][c])
                tr[u][c] = ++tot;
            u = tr[u][c];
        }
    }
};
```

## 模板题目

[P4551 最长异或路径](https://www.luogu.com.cn/problem/P4551)