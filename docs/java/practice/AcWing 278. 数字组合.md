[278. 数字组合](https://www.acwing.com/problem/content/280/)

#### 算法：

*DP* *背包问题*

**简化问题**

- M 看成背包容量；每个数看成一个物品，a[i] 看成体积

- 目标：求出总体积恰好是 M 的方案数

**状态表示 - f(i, j)**

- 集合：所有只从前 i 个物品中选，且总体积恰好是 j 的方案

- 属性：Count

**状态计算 - 集合划分**

以是否选取第 i 个物品来划分 f(i, j) 表示的集合：

- 不包括物品 i 的所有选法：f(i - 1, j)

- 包括物品 i 的所有选法：f(i - 1, j - a[i])

综上，f(i, j) = f(i - 1, j) + f(i - 1, j - a[i])。

**注意**

状态初始化：f(0, 0) = 1, f(0, 1) = f(0, 2) = ... = f(0, m) = 0

#### 时间复杂度度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 10010;
    static int n, m;
    static int[] f = new int[N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        f[0] = 1;
        for (int i = 1; i <= n; i++) {
            int v = sc.nextInt();
            for (int j = m; j >= v; j--) {
                f[j] += f[j - v];
            }
        }

        System.out.println(f[m]);
    }
}
```

