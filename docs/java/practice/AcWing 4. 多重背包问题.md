[4. 多重背包问题 I](https://www.acwing.com/problem/content/4/)

#### 算法：

*#DP#背包问题*

**状态表示 - f(i, j)**

- 集合：从前 i 个物品中选，且总体积不大于 j 的所有选法

- 属性：Max

**状态计算 - 集合划分**

枚举第 i 个物品选几个来划分 f(i, j) 表示的集合：

- 不选第 i 个物品：

- 第 i 个物品选 1 个：

  ...

- 第 i 个物品选 s[i] 个：

分析同完全背包：f(i, j) = max(f(i - 1, j - k * v[i]) + k * w[i])，k ∈ [0, s[i]]。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 110;
    static int n, m;
    static int[] v = new int[N], w = new int[N], s = new int[N];
    static int[][] f = new int[N][N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            v[i] = sc.nextInt();
            w[i] = sc.nextInt();
            s[i] = sc.nextInt();
        }
        
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                for (int k = 0; k <= s[i] && j - k * v[i] >= 0; k++) {
                    f[i][j] = Math.max(f[i][j], f[i - 1][j - k * v[i]] + k * w[i]);
                }
            }
        }
        
        System.out.println(f[n][m]);
    }
}
```

