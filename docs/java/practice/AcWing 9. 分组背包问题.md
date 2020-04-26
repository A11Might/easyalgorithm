[9. 分组背包问题](https://www.acwing.com/problem/content/9/)

#### 算法：

*#DP#背包问题*

**状态表示 - f(i, j)**

- 集合：从前 i 组物品中选，且总体积不大于 j 的所有选法。
- 属性：Max

**状态计算 - 集合划分**

枚举第 i 组物品中选哪个或者不选来划分 f(i, j) 表示的集合：

- 不选第 i 组中的物品：等价于从前 i - 1 组物品中选，且体积不大于 j 的所有选法中价值的最大值，f(i - 1, j)。

- 选第 i 组中的第 1 个物品：

  ...

- 选第 i 组中的第 k 个物品：等价于从前 i - 1 组物品中选，体积不大于 j - v[i] [k] 的所有选法中价值的最大值，再加上第 i 组中的第 k 个物品的价值 w[i] [k]，f(i - 1, j - v[i] [k]]) + w[i] [k]。

综上：f(i, j) = max(f(i - 1, j), f(i - 1, j - v[i] [k]]) + w[i] [k])。

**注：**

- 一个都不选的方案在状态优化成1维的时候就可以省略了，因为本层的f[j]就是上一层的 f[j]。

- 在简化状态表示之前，f[i] [j] 需要从 f[i - 1] [j] 转移过来，如果从小到大循环j，那么在我们计算 f[j] 之前，会先计算 f[j - v[i] [k]]，那么此时的 f[j - v[i] [k]] 就是 f[i] [j - v[i] [k]] 了。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 110;
    static int n, m;
    static int[][] v = new int[N][N], w = new int[N][N];
    static int[] s = new int[N];
    static int[] f = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            s[i] = sc.nextInt();
            for (int j = 0; j < s[i]; j++) {
                v[i][j] = sc.nextInt();
                w[i][j] = sc.nextInt();
            }
        }
        
        for (int i = 1; i <= n; i++) {
            for (int j = m; j >= 0; j--) {
                for (int k = 0; k < s[i]; k++) {
                    if (v[i][k] <= j) {
                        f[j] = Math.max(f[j], f[j - v[i][k]] + w[i][k]);
                    }
                }
            }
        }
        
        System.out.println(f[m]);
    }
}
```

