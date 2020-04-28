[847. 图中点的层次](https://www.acwing.com/problem/content/849/)

#### 算法：

*#bfs*

所有边的长度都是 1 ，使用 bfs 求最短路径。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>
#include <queue>

using namespace std;

const int N = 100010;

int n, m;
int h[N], e[N], ne[N], idx;
int dist[N];

void add(int a, int b) {
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

int main() {
    cin >> n >> m;
    memset(h, -1, sizeof h);
    while (m--) {
        int a, b;
        cin >> a >> b;
        add(a, b);
    }
    
    // 将每个点的距离初始化为 -1，标记为未访问
    memset(dist, -1, sizeof dist);
    
    queue<int> q;
    q.push(1);
    dist[1] = 0;
    while (q.size()) {
        int u = q.front();
        q.pop();
        
        for (int i = h[u]; ~i; i = ne[i]) {
            int j = e[i];
            if (~dist[j]) continue;
            dist[j] = dist[u] + 1;
            q.push(j);
        }
    }
    
    if (~dist[n]) cout << dist[n] << endl;
    else cout << -1 << endl;
    
    return 0;
}
```

