[790. 数的三次方根](https://www.acwing.com/problem/content/792/)

#### 算法：

*#二分搜索*

#### 时间复杂度分析：

每次判断都会将数据规模减少一半，所以最多判断 logn 次，时间复杂度为 O(logn)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

// 精度的经验值是题目要求 +2
const double eps = 1e-8;

int main() {
    double x;
    cin >> x;
    
    double l = -100, r = 100;
    while (r - l > eps) {
        double mid = (l + r) / 2;
        if (mid * mid * mid <= x) l = mid;
        else r = mid;
    }
    
    printf("%.6lf", l);
    
    return 0;
}
```

