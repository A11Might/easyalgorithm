[897. 最长公共子序列](https://www.acwing.com/problem/content/899/)

#### 算法：

*#DP#线性DP*

**状态表示 - f(i, j)**

- 集合：所有第一个序列 a 的前 i 个字符和第二个序列 b 的前 j 个字符的公共子序列。
- 属性：Max

**状态计算 - 集合划分**

- 以字符 a[i] 和 b[j] 是否在公共子序列中来划分 f(i, j) 表示的集合：

  - a[i] 和 b[j] 都不选：f(i - 1, j - 1)。
  - 不选 a[i] 和选 b[j]：不是 f(i - 1, j)，但 f(i - 1, j) 包含这类情况。
  - 选 a[i] 和 不选 b[j]：不是 f(i, j - 1)，但 f(i, j - 1) 包含这类情况。
  - a[i] 和 b[j] 都选：f(i - 1, j - 1) + 1。

  上述四类情况中存在重复部分，但只要不漏就对求最大值没有影响。

- 以字符 a[i] 和 b[i] 是否相等来划分 f(i, j) 表示的集合：

  - 字符 a[i] 和 b[j] 相等：f(i - 1, j - 1) + 1。
  - 字符 a[i] 和 b[j] 不相等：max(f(i - 1, j), f(i, j - 1))。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int n, m;
    static char[] a = new char[N], b = new char[N];
    static int[][] f = new int[N][N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        a = (" " + sc.next()).toCharArray();
        b = (" " + sc.next()).toCharArray();
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (a[i] == b[j]) f[i][j] = f[i - 1][j - 1] + 1;
                else f[i][j] = Math.max(f[i][j - 1], f[i - 1][j]);
            }
        }
        
        System.out.println(f[n][m]);
    }
}
```

