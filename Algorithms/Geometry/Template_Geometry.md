```cpp
namespace Geometry {
    const double EPS = 1e-8;
    bool dcmp(double x, double y = 0) {
        return fabs(x - y) <= EPS;
    }
    struct Point {
        double x, y;
        Point(double x = 0, double y = 0) : x(x), y(y) {}
        Point friend operator+(const Point &a, const Point &b) {
            return Point(a.x + b.x, a.y + b.y);
        }
        Point friend operator-(const Point &a, const Point &b) {
            return Point(a.x - b.x, a.y - b.y);
        }
        double norm() {
            return x * x + y * y;
        }
        friend ostream &operator<<(ostream &output, const Point p) {
            output << "(" << p.x << "," << p.y << ")";
            return output;
        }
    };
    typedef Point Vec;
    double dot(const Vec &a, const Vec &b) {
        return a.x * b.x + a.y * b.y;
    }
    double cross(const Vec &a, const Vec &b) {
        return a.x * b.y - a.y * b.x;
    }
    double dis(const Point &a, const Point &b) {
        return sqrt((a - b).norm());
    }
}
using namespace Geometry;
```