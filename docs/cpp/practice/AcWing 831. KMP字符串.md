[831. KMP字符串](https://www.acwing.com/problem/content/833/)

#### 算法：

*#KMP*

**朴素算法**

```java
for (int i = 1; i <= n; i++ ) {
    bool flag = true;
    for (int j = 1; j <= m; j++ ) {
        if (s[i + j - 1] != p[j]) {
            flag = false;
            break;
        }
    }
}
```

在模式串与主串的匹配过程中，我们可以利用模式串内部的重复性（next 数组），在失配时将模式串向后移动多位，从而减少无意义的匹配。

next[i] 表示模式串中对应字符前的字符串的（除本身外）最长匹配前后缀的长度，也就是 next[i] = j 表示字符串 p[1, j] 和 p[i - j + 1， i] 是相等的。

#### 时间复杂度分析：

- for 循环一共执行 m 次，每次 for 循环中 j 最多 +1，所以 j 最多加 m 次。
- ne[j] 的定义是一定小于 j，所以每次执行 while 循环，j 最少 -1。因为 j 最多加到 m（j == m），所以 while 循环中的 j 最多可以减 m 次。

所以总的时间复杂度是 O(m)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010, M = 1000010;

int n, m;
int ne[N];
char p[N], s[M];

int main() {
    // 下标需要从 1 开始
    cin >> n >> p + 1 >> m >> s + 1;
    
     // 求 next 数组过程
    for (int i = 2, j = 0; i <= n; i++) {
        while (j && p[i] != p[j + 1]) j = ne[j];
        if (p[i] == p[j + 1]) j++;
        ne[i] = j;
    }
    
    // KMP 匹配过程
    for (int i = 1, j = 0; i <= m; i++) {
        while (j && s[i] != p[j + 1]) j = ne[j];
        if (s[i] == p[j + 1]) j++;
        // 匹配成功
        // 出现位置的起始下标为 i - n + 1 需要 -1，因为我们的下标是从 1 开始的
        if (j == n) {
            printf("%d ", i - j);
            j = ne[j];
        }
    }
    
    return 0;
}
```

