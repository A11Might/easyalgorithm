[887. 求组合数 III](https://www.acwing.com/problem/content/889/)

#### 算法：



#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>

using namespace std;

typedef long long LL;

int n;

int qmi(int a, int k, int p) { // 快速幂模板
    int res = 1;
    while (k) {
        if (k & 1) res = (LL)res * a % p;
        a = (LL)a * a % p;
        k >>= 1;
    }
    return res;
}

int C(int a, int b, int p) { // 通过定理求组合数 C(a, b) % p
    if (b > a) return 0;
    
    int ret = 1;
    for (int i = 1, j = a; i <= b; i++, j--) {
        ret = (LL) ret * j % p;
        ret = (LL) ret * qmi(i, p - 2, p) % p;
    }
    
    return ret;
}

int lucas(LL a, LL b, int p) {
    if (a < p && b < p) return C(a, b, p);
    return (LL)C(a % p, b % p, p) * lucas(a / p, b / p, p) % p;
}

int main() {
    cin >> n;
    while (n--) {
        LL a, b;
        int p;
        cin >> a >> b >> p;
        cout << lucas(a, b, p) << endl;;
    }
    
    return 0;
}
```

