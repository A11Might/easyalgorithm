[859. Kruskal算法求最小生成树](https://www.acwing.com/problem/content/861/)

#### 算法：

*#kruskal*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

struct Edge {
    int a, b, w;
    
    bool operator< (const Edge &t)const {
        return w < t.w;
    }
};

const int N = 100010, M = 2 * N;

int n, m;
int p[N];
Edge edges[M];

int find(int x) {
    if (p[x] != x) p[x] = find(p[x]);
    return p[x];
}

int main() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
        cin >> edges[i].a >> edges[i].b >> edges[i].w;
    }
    
    sort(edges, edges + m);
    
    for (int i = 1; i <= n; i++) p[i] = i;
    
    int ret = 0, cnt = 0;
    for (int i = 0; i < m; i++) {
        int a = find(edges[i].a), b = find(edges[i].b);
        if (a != b) {
            p[a] = b;
            ret += edges[i].w;
            cnt++;
        }
    }
    
    if (cnt < n - 1) puts("impossible");
    else cout << ret << endl;
    
    return 0;
}
```

