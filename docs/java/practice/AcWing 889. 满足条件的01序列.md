[889. 满足条件的01序列](https://www.acwing.com/problem/content/891/)

#### 算法：

*#卡特兰数*

将 01 序列置于坐标系中，起点定于原点。若 0 表示向右走，1 表示向上走，那么任何前缀中 0 的个数不少于 1 的个数就转化为：路径上的任意一点，横坐标大于等于纵坐标。题目所求即为这样的合法路径数量。

下图中，表示从 (0, 0) 走到 (n, n) 的路径，在绿线及以下表示合法，若触碰红线即不合法。

![](889.png)

由图可知，任何一条不合法的路径（如黑色路径），都对应一条从 (0, 0) 走到 (n − 1, n + 1) 的一条路径（如灰色路径）。而任何一条 (0, 0) 走到 (n − 1, n + 1) 的路径，也对应了一条从 (0, 0) 走到 (n, n) 的不合法路径。

答案如图，即卡特兰数。

---

作者：番茄酱
链接：https://www.acwing.com/solution/acwing/content/8907/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>

using namespace std;

typedef long long LL;

const int N = 100010, MOD = 1e9 + 7;

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

int main() {
    int n;
    cin >> n;

    int a = n * 2, b = n;
    int ret = 1;
    for (int i = a; i > a - b; i--) ret = (LL)ret * i % MOD;
    for (int i = 1; i <= b; i++) ret = (LL)ret * qmi(i, MOD - 2, MOD) % MOD;

    ret = (LL)ret * qmi(n + 1, MOD - 2, MOD) % MOD;

    cout << ret << endl;

    return 0;
}
```

