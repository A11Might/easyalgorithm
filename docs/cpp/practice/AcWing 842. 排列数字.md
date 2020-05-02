[842. 排列数字](https://www.acwing.com/problem/content/844/)

#### 算法：

*#dfs#暴搜*

依次枚举每个位置上填写的数字。

#### 时间复杂度分析：



#### 代码

```cpp
#include <iostream>

using namespace std;

const int N = 10;

int n;
int path[N];

// 由于题目数据范围是 1 ≤ n ≤ 7，可以使用整型变量 state 代替布尔数组
void dfs(int u, int state) {
    if (u == n) {
        for (int i = 0; i < n; i ++ ) cout << path[i] << ' ';
        cout << endl;
        return;
    }

    // 枚举当前位置上填写的数字
    for (int i = 0; i < n; i ++ ) {
        if (!(state >> i & 1)) {
            path[u] = i + 1;
            dfs(u + 1, state + (1 << i));
        }
    }
}

int main() {
    cin >> n;

    dfs(0, 0);

    return 0;
}
```

