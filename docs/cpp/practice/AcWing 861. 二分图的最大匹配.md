[861. 二分图的最大匹配](https://www.acwing.com/problem/content/863/)

#### 算法：

*#匈牙利算法*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 510, M = 100010;

int n1, n2, m;
int h[N], e[M], ne[M], idx;
int match[N];
bool st[N];

void add(int a, int b) {
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

bool find(int x) {
    for (int i = h[x]; ~i; i = ne[i]) {
        int j = e[i];
        if (!st[j]) {
            st[j] = true;
            if (!match[j] || find(match[j])) {
                match[j] = x;
                return true;
            }
        }
    }
    
    return false;
}

int main() {
    cin >> n1 >> n2 >> m;
    
    memset(h, -1, sizeof h);
    while (m--) {
        int a, b;
        cin >> a >> b;
        add(a, b);
    }
    
    int ret = 0;
    for (int i = 1; i <= n1; i++) {
        memset(st, 0, sizeof st);
        if (find(i)) ret++;
    }
    cout << ret << endl;
    
    return 0;
}
```

