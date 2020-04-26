[3. 完全背包问题](https://www.acwing.com/problem/content/3/)

#### 算法：

*#DP#背包问题*

**状态表示 - f(i, j)**

- 集合：从前 i 个物品中选，且总体积不大于 j 的所有选法。
- 属性：Max

**状态计算 - 集合划分**

枚举第 i 个物品选几个来划分 f(i, j) 表示的集合：

- 第 i 个物品选 0 个：从前 i 个物品中选并且不选第 i 个物品，总体积不大于 j 的所有选法中总价值的最大值。

  等价于所有只考虑前 i - 1 个物品，且总体积不大于 j 的所有选法中总价值的最大值，f(i - 1, j)。

- 第 i 个物品选 1 个

  ...

- 第 i 个物品选 k 个：从前 i 个物品中选并且选 k 个第 i 个物品，总体积不大于 j 的所有选法中总价值的最大值。

  因为每种选法中都包含 k 个第 i 个物品，所以我们可以先考虑除第 i 个物品外，前 i - 1 个物品的选法，也就是从前 i - 1 个物品中选，且总体积不大于 j - k * v[i] 的所有选法，然后再加上 k * w[i]，f(i - 1, j - k * v[i]) + k * w[i]。

综上：f(i, j) = max(f(i - 1, j - k * v[i]) + k * w[i])。

**优化：**

由

f(i, j) 	 = max(f(i - 1, j), f(i - 1, j - v[i]) + w[i], f(i - 1, j - 2 * v[i]) + 2 * w[i], f(i - 1, j - 3 * v[i]) + 3 * w[i], ...)

f(i, j - v[i]) = max(           f(i - 1, j - v[i]),            f(i - 1, j - 2 * v[i]) + w[i], 	  f(i - 1, j - 3 * v[i]) + 2 * w[i], ...) 

可以化简得到

f(i , j) = max(f(i - 1, j), f(i, j - v[i]) + w[i])

f(i, j) 都是从第 i 层、第 i - 1 层转移过来的，所以可以使用滚动数组优化，删除一维。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int n, m;
    static int[] v = new int[N], w = new int[N];
    static int[] f = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            v[i] = sc.nextInt();
            w[i] = sc.nextInt();
        }
        
        for (int i = 1; i <= n; i++) {
            for (int j = v[i]; j <= m; j++) {
                f[j] = Math.max(f[j], f[j - v[i]] + w[i]); 
            }
        }
        
        System.out.println(f[m]);
    }
}
```

