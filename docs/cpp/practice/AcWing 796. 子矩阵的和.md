[796. 子矩阵的和](https://www.acwing.com/problem/content/798/)

#### 算法：

*#前缀和*

#### 时间复杂度分析：

预处理前缀和需要遍历一遍矩阵，时间复杂度为 O(n * m)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1010;

int n, m, k;
int s[N][N];

int main() {
    cin >> n >> m >> k;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            scanf("%d", &s[i][j]);
            s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + s[i][j]; // 初始化二维前缀和
        }
    }
    
    while (k--) {
        int x1, y1, x2, y2;
        scanf("%d%d%d%d", &x1, &y1, &x2, &y2);
        printf("%d\n", s[x2][y2] - s[x2][y1 - 1] - s[x1 - 1][y2] + s[x1 - 1][y1 - 1]); // 计算子矩阵和
    }
    
    return 0;
}
```

