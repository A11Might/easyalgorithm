[891. Nim游戏](https://www.acwing.com/problem/content/893/)

#### 算法：

*Nim 游戏*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>

using namespace std;

int main() {
    int n;
    cin >> n;
    
    int ret = 0;
    while (n--) {
        int a;
        cin >> a;
        ret ^= a;
    }
    
    if (ret) puts("Yes");
    else puts("No");
    
    return 0;
}
```

