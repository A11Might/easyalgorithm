[849. Dijkstra求最短路 I](https://www.acwing.com/problem/content/851/)

#### 算法：

*#dijkstra*

题目给定的数据范围数据：1 ≤ 节点数 ≤ 500，1 ≤ 边数 ≤10<sup>51</sup>。表示的图是稠密图，所以使用朴素 Dijkstra 算法。

#### 时间复杂度分析：

时间复杂是 O(n<sup>2</sup> + m)，n 表示点数，m 表示边数。

#### 代码：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 510, M = 100010;

int n, m;
int g[N][N];
int dist[N];
bool st[N];

int main() {
    cin >> n >> m;
    memset(g, 0x3f, sizeof g);
    while (m--) {
        int a, b, c;
        cin >> a >> b >> c;
        g[a][b] = min(g[a][b], c);
    }
    
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    for (int i = 0; i < n - 1; i++) {
        int t = -1;
        for (int j = 1; j <= n; j++) {
            if (!st[j] && (t == -1 || dist[j] < dist[t])) t = j;
        }
        st[t] = true;
        
        for (int j = 1; j <= n; j++) {
            dist[j] = min(dist[j], dist[t] + g[t][j]);
        }
    }
    
    if (dist[n] == 0x3f3f3f3f) cout << -1 << endl;
    else cout << dist[n] << endl;
    
    return 0;
}
```

