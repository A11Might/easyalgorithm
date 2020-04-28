[860. 染色法判定二分图](https://www.acwing.com/problem/content/862/)

#### 算法：

*#染色法*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 100010, M = 2 * N;

int n, m;
int h[N], e[M], ne[M], idx;
int color[N];

void add(int a, int b) {
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

bool dfs(int x, int c) {
    color[x] = c;
    
    for (int i = h[x]; ~i; i = ne[i]) {
        int j = e[i];
        if (!color[j]) {
            if (!dfs(j, 3 - c)) return false;
        } else if (color[j] == c) return false;
    }
    return true;
}

int main() {
    cin >> n >> m;
    
    memset(h, -1, sizeof h);
    while (m--) {
        int a, b;
        cin >> a >> b;
        add(a, b), add(b, a);
    }
    
    for (int i = 1; i <= n; i++) {
        if (!color[i]) {
            if (!dfs(i, 1)) {
                puts("No");
                return 0;
            }
        }
    }
    puts("Yes");
    return 0;
}
```

