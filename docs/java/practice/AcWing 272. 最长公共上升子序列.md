[272. 最长公共上升子序列](https://www.acwing.com/problem/content/274/)

#### 算法：

*DP* *LIS* *LCS*

**状态表示 - f(i, j)**

- 集合：所有由 `第一个序列的前 i 个字母和第二个序列的前 j 个字母构成的`，且 `以 b[j] 结尾` 的公共上升子序列。

  这样可以同时考虑公共子序列和上升子序列。

- 属性：Max

**状态计算 - 集合划分**

以是否包含 a[i] 来划分 f(i, j) 表示的集合：

- 所有不包含 a[i] 的公共上升子序列：f(i - 1, j)

- 所有包含 a[i] 的公共上升子序列

  以倒数第二个数是哪个来划分所有包含 a[i] 的公共上升子序列表示的集合：
  
  - 没有倒数第二个数：1

  - 倒数第二个数是 b[1]

  - 倒数第二个数是 b[2]

    ...

  - 倒数第二个数是 b[k]：f(i - 1, k) + 1

综上，f(i, j) = max(f(i - 1, j), f(i - 1, k) + 1)。

**优化**

如果直接按上述思路实现，需要三重循环：

```java
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        f[i][j] = f[i - 1][j];
        if (a[i] == b[j]) {
            f[i][j] = Math.max(f[i][j], 1);
            for (int k = 1; k < j; k++) { // <---
                if (b[k] < b[j]) f[i][j] = max(f[i][j], f[i - 1][k] + 1);
            }
        }
    }
}
```

因为 a[i] == b[j]，所以我们可以将 b[j] 替换成 a[i]，这样最内层循环就是找到求满足 b[k] < a[i] 的 f\[i - 1][k] + 1 的前缀（从 1 到 j - 1）的最大值，可以发现 b[k] < a[i] 这个条件与是 j 没有关系的。

在满足一个和 j 没有关系的条件的前提下，求某个前缀的最大值，常用的优化方式是：使用一个变量来存储前缀的最大值，边循环边求，这样可以省去一维循环。

最终答案枚举子序列结尾取最大值即可。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 3010;
    static int n;
    static int[] a = new int[N], b = new int[N];
    static int[][] f = new int[N][N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        for (int i = 1; i <= n; i++) a[i] = sc.nextInt();
        for (int i = 1; i <= n; i++) b[i] = sc.nextInt();

        for (int i = 1; i <= n; i++) {
            int maxv = 1;
            for (int j = 1; j <= n; j++) {
                f[i][j] = f[i - 1][j];
                if (a[i] == b[j]) f[i][j] = Math.max(f[i][j], maxv);
                if (b[j] < a[i]) maxv = Math.max(maxv, f[i - 1][j] + 1);
            }
        }

        int ret = 0;
        for (int i = 1; i <= n; i++) ret = Math.max(ret, f[n][i]);
        System.out.println(ret);
    }
}
```

