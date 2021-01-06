[873. 欧拉函数](https://www.acwing.com/problem/content/875/)

#### 算法：

*#欧拉函数*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>

using namespace std;

int main() {
    int n;
    cin >> n;
    while (n--) {
        int x;
        cin >> x;
        
        int ret = x;
        for (int i = 2; i <= x / i; i++) {
            if (x % i == 0) {
                ret = ret / i * (i - 1);
                while (x % i == 0) x /= i;
            }
        }
        
        if (x > 1) ret = ret / x * (x - 1);
        
        cout << ret << endl;
    }
    
    return 0;
}
```

