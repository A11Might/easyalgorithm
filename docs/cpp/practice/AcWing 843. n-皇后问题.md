[843. n-皇后问题](https://www.acwing.com/problem/content/description/845/)

#### 算法：

*#dfs#暴搜*

依次枚举每个位置上是否放置皇后。

#### 时间复杂度分析：

时间复杂度为 O(2<sup>n <sup>2</sup></sup>)。

#### 代码：

```cpp
#include <iostream>

using namespace std;

const int N = 10;

int n;
int row[N]; // 记录每一行上皇后的放置位置
bool col[N], dia1[2 * N], dia2[2 * N];

void dfs(int u) {
    if (u == n) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (row[i] == j) cout << "Q";
                else cout << ".";
            }
            cout << endl;
        }
        cout << endl;
        return;
    }
    // 枚举当前行上皇后放置位置
    for (int i = 0; i < n; i++) {
        if (col[i] || dia1[u + i] || dia2[u - i + n]) continue;
        col[i] = dia1[u + i] = dia2[u - i + n] = true;
        row[u] = i;
        dfs(u + 1);
        col[i] = dia1[u + i] = dia2[u - i + n] = false;
    }
}

int main() {
    cin >> n;
    dfs(0);
    
    return 0;
}
```

