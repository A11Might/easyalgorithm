[886. 求组合数 II](https://www.acwing.com/problem/content/888/)

#### 算法：

*#通过预处理逆元的方式求组合数*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>

using namespace std;

typedef long long LL;

const int N = 100010, MOD = 1e9 + 7;

int n;
int fact[N], infact[N];

int qmi(int a, int k, int p) { // 快速幂模板
    int res = 1;
    while (k) {
        if (k & 1) res = (LL)res * a % p;
        a = (LL)a * a % p;
        k >>= 1;
    }
    return res;
}

int main() {
    fact[0] = infact[0] = 1;
    for (int i = 1; i < N; i++) {
        fact[i] = (LL)fact[i - 1] * i % MOD;
        infact[i] = (LL)infact[i - 1] * qmi(i, MOD - 2, MOD) % MOD;
    }
    
    cin >> n;
    while (n--) {
        int a, b;
        cin >> a >> b;
        cout << (LL)fact[a] * infact[b] % MOD * infact[a - b] % MOD << endl;
    }
    
    return 0;
}
```

