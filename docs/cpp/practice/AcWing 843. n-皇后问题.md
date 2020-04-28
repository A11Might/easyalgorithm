[843. n-皇后问题](https://www.acwing.com/problem/content/description/845/)

#### 算法：

*#dfs#暴搜*

依次枚举每个位置上是否放置皇后。

#### 时间复杂度分析：

时间复杂度为 O(2<sup>n <sup>2</sup></sup>)。

#### 代码：

```cpp
#include <iostream>

using namespace std;

const int N = 10, M = 2 * N;

int n;
char g[N][N];
bool col[N], dg[M], udg[M];

void dfs(int u) {
    if (u == n) {
        for (int i = 0; i < n; i ++ ) puts(g[i]);
        puts("");
        return;
    }
    
    // 枚举当前行上皇后放置位置
    for (int i = 0; i < n; i ++ ) {
        if (!col[i] && !dg[u + i] && !udg[n - u + i]) {
            g[u][i] = 'Q';
            col[i] = dg[u + i] = udg[n - u + i] = true;
            dfs(u + 1);
            col[i] = dg[u + i] = udg[n - u + i] = false;
            g[u][i] = '.';
        }
    }
}

int main() {
    cin >> n;
    for (int i = 0; i < n; i ++ )
        for (int j = 0; j < n; j ++ )
            g[i][j] = '.';

    dfs(0);

    return 0;
}
```

