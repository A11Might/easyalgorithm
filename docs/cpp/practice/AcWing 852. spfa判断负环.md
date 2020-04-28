[852. spfa判断负环](https://www.acwing.com/problem/content/854/)

#### 算法：

*#spfa*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>
#include <queue>

using namespace std;

const int N = 2010, M = 100010;

int n, m;
int h[N], w[M], e[M], ne[M], idx;
int dist[N], cnt[N]; // cnt[x]存储 1 到 x 的最短路中经过的点数
bool st[N];

void add(int a, int b, int c) {
    e[idx] = b, w[idx] = c, ne[idx] = h[a], h[a] = idx++;
}

int main() {
    cin >> n >> m;
    memset(h, -1, sizeof h);
    while (m--) {
        int a, b, c;
        cin >> a >> b >> c;
        add(a, b, c);
    }
    
    queue<int> q;
    for (int i = 1; i <= n; i++) {
        q.push(i);
        st[i] = true;
    }
    while (q.size()) {
        int u = q.front();
        q.pop();
        st[u] = false;
        
        for (int i = h[u]; ~i; i = ne[i]) {
            int j = e[i];
            if (dist[j] > dist[u] + w[i]) {
                dist[j] = dist[u] + w[i];
                cnt[j] = cnt[u] + 1;
                // 如果从 1 号点到 x 的最短路中包含至少 n 个点（不包括自己），则说明存在环
                if (cnt[j] >= n) {
                    puts("Yes");
                    return 0;
                }
                if (!st[j]) {
                    st[j] = true;
                    q.push(j);
                }
            }
        }
    }
    puts("No");
    return 0;
}
```

