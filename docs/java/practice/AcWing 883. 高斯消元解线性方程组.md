[883. 高斯消元解线性方程组](https://www.acwing.com/problem/content/885/)

#### 算法：

*#高斯消元*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cmath>

using namespace std;

const int N = 110;
const double eps = 1e-6;

int n;
double a[N][N];

int gauss() {
    int r, c;
    for (r = 0, c = 0; c < n; c++) {
        int t = r;
        for (int i = r + 1; i < n; i++) { // 找到绝对值最大的行
            if (fabs(a[i][c]) > fabs(a[t][c])) t = i;
        }
        
        if (fabs(a[t][c]) < eps) continue;
        
        // 将绝对值最大的行换到最顶端
        for (int i = c; i <= n; i++) swap(a[r][i], a[t][i]);
        
        // 将当前上的首位变成 1
        for (int i = n; i >= c; i--) a[r][i] /= a[r][c];
        
        // 用当前行将下面所有的列消成 0
        for (int i = r + 1; i < n; i++) {
            if (fabs(a[i][c]) < eps) continue;
            for (int j = n; j >= c; j--) {
                a[i][j] -= a[r][j] * a[i][c]; 
            }
        }
        
        r++;
    }
    
    if (r < n) {
        for (int i = r; i < n; i++) {
            if (fabs(a[i][n]) > eps) return 2; // 无解
        }
        return 1; // 有无穷多组解
    }
    
    for (int i = n - 1; i >= 0; i--) {
        for (int j = i + 1; j < n; j++) {
            a[i][n] -= a[i][j] * a[j][n];
        }
    }
    return 0; // 有唯一解
}

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j <= n; j++) {
            cin >> a[i][j];
        }
    }
    
    int ret = gauss();
    
    if (ret == 0) {
        for (int i = 0; i < n; i++) printf("%.2lf\n", a[i][n]);
    } else if (ret == 1) puts("Infinite group solutions");
    else puts("No solution");
    
    return 0;
}
```

