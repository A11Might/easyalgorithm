[853. 有边数限制的最短路](https://www.acwing.com/problem/content/855/)

#### 算法：

*#bellman - ford*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

struct Edge {
    int a, b, w;
};

const int N = 510, M = 10010;

int n, m, k;
int dist[N], backup[N];
Edge edges[M];

int main() {
    cin >> n >> m >> k;
    for (int i = 0; i < m; i++) {
        cin >> edges[i].a >> edges[i].b >> edges[i].w;
    }
    
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    for (int i = 0; i < k; i++) {
        // 备份 dist 数组，当前循环中的更新操作使用上次更新的结果，防止串连
        memcpy(backup, dist, sizeof dist);
        for (int j = 0; j < m; j++) {
            auto e = edges[j];
            dist[e.b] = min(dist[e.b], backup[e.a] + e.w);
        }
    }
    
    // 负权边可能会更新 0x3f3f3f3f 的值
    if (dist[n] > 0x3f3f3f3f / 2) puts("impossible");
    else cout << dist[n] << endl;
    
    return 0;
}
```

