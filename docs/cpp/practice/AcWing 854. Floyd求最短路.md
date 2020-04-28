[854. Floyd求最短路](https://www.acwing.com/problem/content/856/)

#### 算法：

*#floyd*

#### 时间复杂度分析：



#### 代码：

```c++
#include <iostream>
#include <cstring>

using namespace std;

const int N = 210, M = 20010;

int n, m, k;
int d[N][N];

int main() {
    cin >> n >> m >> k;
    
    // 去掉重边和自环
    memset(d, 0x3f, sizeof d);
    for (int i = 1; i <= n; i++) d[i][i] = 0;
    while (m--) {
        int a, b, w;
        cin >> a >> b >> w;
        d[a][b] = min(d[a][b], w);
    }
    
    for (int k = 1; k <= n; k++) {
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                d[i][j] = min(d[i][j], d[i][k] + d[k][j]);
            }
        }
    }
    
    while (k--) {
        int a, b;
        cin >> a >> b;
        if (d[a][b] > 0x3f3f3f3f / 2) puts("impossible");
        else cout << d[a][b] << endl;
    }
    
    return 0;
}
```

