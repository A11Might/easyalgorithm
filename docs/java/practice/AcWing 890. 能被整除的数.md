[890. 能被整除的数](https://www.acwing.com/problem/content/892/)

#### 算法：

*#容斥原理*

将 1 ~ n 中能被 a 整除的数的个数记作 S<sub>a</sub>，能被 b 整除的数的个数记作 S<sub>b</sub>，那么 1 ~ n 能被 a 或者 b 整除的数的个数就是 |S<sub>a</sub> ∪ S<sub>b</sub>| = |S<sub>a</sub>| + |S<sub>b</sub>| - |S<sub>a</sub> ∩ S<sub>b</sub>|（求并集，集合间可能会有重复的元素，需要去重）。

其中 |S<sub>p</sub>| 表示 1 ~ n 中能被 p 整除的数的个数，也就是 1 ~ n 中 p 的倍数的个数，求法是 S<sub>p</sub> = ⌊n / p⌋；|S<sub>p<sub>1</sub></sub> ∩ S<sub>p<sub>2</sub></sub> ∩ ... ∩ <sub>p<sub>k</sub></sub>| 表示 1 ~ n 中既能被 p<sub>1</sub> 也能 p<sub>2</sub>，又能 p<sub>3</sub> ... 整除的数的个数，因为给定的数是质数，它们两两互质，所以既能被 p<sub>1</sub> 也能 p<sub>2</sub>，又能 p<sub>3</sub> ... 整除的数就是能被 p<sub>1</sub> * p<sub>2</sub> * ... * p<sub>k</sub> 整除的数的个数，求法是 |S<sub>p<sub>1</sub></sub> ∩ S<sub>p<sub>2</sub></sub> ∩ ... ∩ <sub>p<sub>k</sub></sub>| = ⌊n / (p<sub>1</sub> * p<sub>2</sub> * ... * p<sub>k</sub>)⌋。

由上我们可以知道，1 ~ n 中能被 p<sub>1</sub> 或者 p<sub>2</sub> 或者 ... p<sub>m</sub> 整除的数的个数就是：

|S<sub>p<sub>1</sub></sub> ∪ S<sub>p<sub>2</sub></sub> ∪ ... ∪ S<sub>p<sub>m</sub></sub> | = 

|S<sub>p<sub>1</sub></sub>| + |S<sub>p<sub>2</sub></sub>| + |S<sub>p<sub>3</sub></sub>| + ...

-|S<sub>p<sub>1</sub></sub> ∩ S<sub>p<sub>2</sub></sub>| - |S<sub>p<sub>1</sub></sub> ∩ S<sub>p<sub>3</sub></sub>| - |S<sub>p<sub>2</sub></sub> ∩ S<sub>p<sub>3</sub></sub>| -

+|S<sub>p<sub>1</sub></sub> ∩ S<sub>p<sub>2</sub></sub> ∩ S<sub>p<sub>3</sub></sub>| + ... +

-...

所以我们需要**枚举所有集合组合的情况，一般使用位运算枚举**：从 m 个集合中选任意多个集合（除 0 个外），一共 2<sup>m</sup> - 1 中情况，从 1 枚举到 2<sup>m</sup> - 1，把每个数字看成 m 位的二进制数，每一位都表示该位对应的集合是否选取，奇数个集合时取正号，偶数个集合时取负号。

#### 时间复杂度分析：

计算每个集合 |S<sub>p<sub>1</sub></sub> ∩ S<sub>p<sub>2</sub></sub> ∩ ... ∩ <sub>p<sub>k</sub></sub>| = ⌊n / (p<sub>1</sub> * p<sub>2</sub> * ... * p<sub>k</sub>)⌋ 的时间复杂度是 O(k)，一共有 2<sup>m</sup> 个集合，所以总时间复杂度就是 O(m * 2<sup>m</sup>)。

#### 代码：

```cpp
#include <iostream>

using namespace std;

typedef long long LL;

const int N = 20;

int n, m;
int h[N];

int main() {
    cin >> n >> m;
    for (int i = 0; i < m; i++) cin >> h[i];
    
    int ret = 0;
    for (int i = 1; i < 1 << m; i++) {
        LL t = 1;
        int cnt = 0;
        for (int j = 0; j < m; j++) {
            if (i >> j & 1) {
                cnt++;
                t *= h[j];
                if (t > n) {
                    t = -1;
                    break;
                }
            }
        }
        if (~t) {
            if (cnt % 2) ret += n / t;
            else ret -= n / t;
        }
    }
    
    cout << ret << endl;
    
    return 0;
}
```

