[848. 有向图的拓扑序列](https://www.acwing.com/problem/content/850/)

#### 算法：

*#拓扑排序*

#### 时间复杂度分析：

时间复杂度 O(n + m)，n 表示点数，m 表示边数。

#### 代码：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 100010;

int n, m;
int h[N], e[N], ne[N], idx;
int d[N];
int q[N], hh, tt;

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
        d[b]++;
    }
    
    hh = 0, tt = -1;
    for (int i = 1; i <= n; i++) {
        if (!d[i]) q[++tt] = i;
    }
    while (hh <= tt) {
        int u = q[hh++];
        for (int i = h[u]; ~i; i = ne[i]) {
            int j = e[i];
            if (--d[j] == 0) q[++tt] = j;
        }
    }
    
    if (tt == n - 1) {
        for (int i = 0; i < n; i++) cout << q[i] << ' ';
    } else cout << -1 << endl;
    
    return 0;
}
```

