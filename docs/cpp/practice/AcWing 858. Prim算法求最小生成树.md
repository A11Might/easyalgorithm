[858. Prim算法求最小生成树](https://www.acwing.com/problem/content/860/)

#### 算法：

*#prim*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 510, M = 100010, INF = 0x3f3f3f3f;

int n, m;
int g[N][N];
int dist[N];
bool st[N];

int main() {
    cin >> n >> m;
    
    memset(g, 0x3f, sizeof g);
    while (m--) {
        int a, b, w;
        cin >> a >> b >> w;
        g[a][b] = g[b][a] = min(g[a][b], w);
    }
    
    int ret = 0;
    memset(dist, 0x3f, sizeof dist);
    for (int i = 0; i < n; i++) {
        int t = -1;
        for (int j = 1; j <= n; j++) {
            if (!st[j] && (t == -1 || dist[j] < dist[t])) t = j;
        }
        if (i && dist[t] == INF) {
            puts("impossible");
            return 0;
        }
        if (i) ret += dist[t];
        st[t] = true;
        
        for (int j = 1; j <= n; j++) dist[j] = min(dist[j], g[j][t]);
    }
    
    cout << ret << endl;
    return 0;
}
```

