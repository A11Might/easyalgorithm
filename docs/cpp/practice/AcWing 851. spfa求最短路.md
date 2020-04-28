[851. spfa求最短路](https://www.acwing.com/problem/content/853/)

#### 算法：

*#spfa*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>
#include <queue>

using namespace std;

const int N = 100010;

int n, m;
int h[N], w[N], e[N], ne[N], idx;
int dist[N];
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
    q.push(1);
    st[1] = true;
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    
    while (q.size()) {
        int u = q.front();
        q.pop();
        st[u] = false;
        
        for (int i = h[u]; ~i; i = ne[i]) {
            int j = e[i];
            if (dist[j] > dist[u] + w[i]) {
                dist[j] = dist[u] + w[i];
                if (!st[j]) {
                    st[j] = true;
                    q.push(j);
                }
            }
        }
    }
    
    if (dist[n] == 0x3f3f3f3f) puts("impossible");
    else cout << dist[n] << endl;
    
    return 0;
}
```

