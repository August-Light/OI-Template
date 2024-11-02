# Graham

## 代码

时间复杂度 $O(n \log n)$。

```cpp
vector<Point> get_convex() {
    vector<Point> points;
    int id = 1;
    for (int i = 1; i <= n; i++)
        if (a[i].x < a[id].x || (a[i].x == a[id].x && a[i].y < a[id].y))
            id = i;
    if (id != 1) std::swap(a[1], a[id]);

    auto o = a[1];
    sort(a+2, a+n+1, [&](const Point &a, const Point &b) {
        Vec va = a - o, vb = b - o;
        double t = cross(va, vb);
        if (!dcmp(t))
            return t > 0;
        return va.norm() < vb.norm();
    });

    points.push_back(o);
    for (int i = 2; i <= n; i++) {
        while (points.size() >= 2 &&
                cross(a[i] - points[points.size() - 2],
                    points.back() - points[points.size() - 2]) >= 0)
            points.pop_back();
        points.push_back(a[i]);
    }
    points.push_back(o);
    return points;
}
```

## 模板题目

[P2742 [USACO5.1] 圈奶牛Fencing the Cows /【模板】二维凸包](https://www.luogu.com.cn/problem/P2742)