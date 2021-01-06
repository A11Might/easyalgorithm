[2. 01背包问题](https://www.acwing.com/problem/content/2/)

#### 算法：

*#DP#背包问题*

**背包问题分类**

1. 01背包：每件物品最多只能使用一次

2. 完全背包：每件物品可以使用无限次

3. 多重背包：每件物品可以使用 s<sub>i</sub> 次

4. 分组背包：每组物品中最多只能选一种物品

**状态表示 - f(i, j)**

- 集合：从前 i 个物品中选，且总体积不大于 j 的所有选法

- 属性：Max

**状态计算 - 集合划分**

枚举是否选取第 i 个物品来划分 f(i, j) 表示的集合：

- 不包含 i 的选法：从前 i 个物品中选并且不包含第 i 个物品，总体积不大于 j 的所有选法中总价值的最大值。

  也就是从前 i - 1 个物品中选，总体积不大于 j 的所有选法中总价值的最大值：f(i - 1, j)。

- 包含 i 的选法：从前 i 个物品中选并且包含第 i 个物品，总体积不大于 j 的所有选法中总价值的最大值。

  因为每种选法都包含第 i 个物品，所以我们可以先考虑除第 i 个物品外，前 i - 1 个物品的选法，也就是从前 i - 1 个物品中选，总体积不大于 j - w<sub>i</sub> 的所有选法中总价值的最大值，然后再加上第 i 个物品的价值：f(i - 1, j - v<sub>i</sub>) + w<sub>i</sub>。
  
  这个子集可能是空集，因为当前背包可能放不下第 i 件物品 - j 可能小于 v<sub>i</sub>，需要判断。

综上：f(i, j) = max(f(i - 1, j), f(i - 1, j - v<sub>i</sub>) + w<sub>i</sub>)。

**优化：**

- f(i, j) 都是从第 i - 1 层转移过来的，所以可以使用滚动数组优化。

- 状态转移使用的是上一层的状态时，我们就从大到小枚举体积。

  这样可以保证计算当前状态时所用到的体积没有被计算过，存的是上一层的状态。

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
            for (int j = m; j >= v[i]; j--) {
                f[j] = Math.max(f[j], f[j - v[i]] + w[i]);
            }
        }
        
        System.out.println(f[m]);
    }
}
```

