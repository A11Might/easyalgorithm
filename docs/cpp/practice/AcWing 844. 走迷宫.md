[844. 走迷宫](https://www.acwing.com/problem/content/846/)

#### 算法：

*#bfs*

**拓展 - 打印路径**

记录每个位置是从哪个位置走过来的，然后倒着往前推就行了。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>
#include <queue>

using namespace std;

typedef pair<int, int> PII;

const int N = 110;

int n, m;
int g[N][N], d[N][N];
int dx[] = {-1, 0, 1, 0}, dy[] = {0, 1, 0, -1};

int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            cin >> g[i][j];
        }
    }
    
    memset(d, -1, sizeof d);
    
    queue<PII> q;
    q.push({1, 1});
    d[1][1] = 0;
    while (q.size()) {
        auto u = q.front();
        q.pop();
        int x = u.first, y = u.second;
        for (int i = 0; i < 4; i++) {
            int a = x + dx[i], b = y + dy[i];
            if (a < 1 || a > n || b < 1 || b > m || g[a][b] == 1 || ~d[a][b]) continue;
            d[a][b] = d[x][y] + 1;
            q.push({a, b});
        }
    }
    
    cout << d[n][m] << endl;
    
    return 0;
}
```

**打印路径**

```cpp
#include <iostream>
#include <cstring>
#include <queue>

using namespace std;

typedef pair<int, int> PII;

const int N = 110;

int n, m;
int g[N][N], d[N][N];
int dx[] = {-1, 0, 1, 0}, dy[] = {0, 1, 0, -1};
int pre[N][N][2];

int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            cin >> g[i][j];
        }
    }
    
    memset(d, -1, sizeof d);
    
    queue<PII> q;
    q.push({1, 1});
    d[1][1] = 0;
    while (q.size()) {
        auto u = q.front();
        q.pop();
        int x = u.first, y = u.second;
        for (int i = 0; i < 4; i++) {
            int a = x + dx[i], b = y + dy[i];
            if (a < 1 || a > n || b < 1 || b > m || g[a][b] == 1 || ~d[a][b]) continue;
            d[a][b] = d[x][y] + 1;
            pre[a][b][0] = x, pre[a][b][1] = y;
            q.push({a, b});
        }
    }
    
    cout << d[n][m] << endl;
    
    int i = n, j = m;
    while (i != 1 || j != 1) {
        cout << i << ' ' << j << endl;
        auto p = pre[i][j];
        i = p[0];
        j = p[1];
    }
    
    return 0;
}
```

