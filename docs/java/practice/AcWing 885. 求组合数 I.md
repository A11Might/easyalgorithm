[885. 求组合数 I](https://www.acwing.com/problem/content/887/)

#### 算法：

*#递归法求组合数*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>

using namespace std;

const int N = 2010, MOD = 1e9 + 7;

int n;
int c[N][N];

void init() { // 通过递推公式预处理组合数
    for (int i = 0; i < N; i++) {
        for (int j = 0; j <= i; j++) {
            if (!j) c[i][j] = 1;
            else c[i][j] = (c[i - 1][j] + c[i - 1][j - 1]) % MOD;
        }
    }
}

int main() {
    cin >> n;
    
    init();
    while (n--) {
        int a, b;
        cin >> a >> b;
        cout << c[a][b] << endl;
    }
    
    return 0;
}
```

