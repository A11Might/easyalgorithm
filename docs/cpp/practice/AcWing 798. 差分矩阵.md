[798. 差分矩阵](https://www.acwing.com/problem/content/description/800/)

#### 算法：

*#差分*

#### 时间复杂度分析：

插入操作的时间复杂度为 O(1)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1010;

int n, m, q;
int b[N][N];

void insert(int x1, int y1, int x2, int y2, int x) {
    b[x1][y1] += x;
    b[x1][y2 + 1] -= x, b[x2 + 1][y1] -= x;
    b[x2 + 1][y2 + 1] +=x;
}

int main() {
    scanf("%d%d%d", &n, &m, &q);
    
    // 构建差分矩阵
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            int x;
            scanf("%d", &x);
            insert(i, j, i, j, x);
        }
    }
    
    // q 次子矩阵加 c 操作
    while (q--) {
        int x1, y1, x2, y2, c;
        scanf("%d%d%d%d%d", &x1, &y1, &x2, &y2, &c);
        insert(x1, y1, x2, y2, c);
    }
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            // 求差分矩阵的二维前缀和 
            b[i][j] = b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1] + b[i][j];
            printf("%d ", b[i][j]);
        }
        puts("");
    }
    
    return 0;
}
```

