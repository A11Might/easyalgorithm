[1023. 买书](https://www.acwing.com/problem/content/1025/)

#### 算法：

*DP* *背包问题*

**状态表示 - f(i, j)**

- 集合：所有只从前 i 个物品中选，且总体积恰好是 j 的方案

- 属性：Count

**状态计算 - 集合划分**

以第 i 个物品选几个来划分 f(i, j) 表示的集合：

- 不选第 i 个物品：f(i - 1, j)

- 选 1 个第 i 个物品

  ...

- 选 k 个第 i 个物品：f(i - 1, j - k * v[i])

综上，f(i, j) = f(i - 1, j) + f(i - 1, j - v[i]) + f(i - 1, j - 2 * v[i]) + ... + f(i - 1, j - k * v[i])。

**优化**

> f(i, j) = f(i - 1, j) + f(i - 1, j - v[i]) + f(i - 1, j - 2 * v[i]) + ... + f(i - 1, j - k * v[i])
>
> f(i, j - v[i]) = f(i - 1, j - v[i]) + f(i - 1, j - 2 * v[i]) + ... + f(i - 1, j - k * v[i])

可以得到 f(i, j) = f(i - 1, j) + f(i, j - v[i])。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int m;
    static int[] v = {10, 20, 50, 100};
    static int[] f = new int[N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        m = sc.nextInt();

        f[0] = 1;
        for (int i = 0; i < 4; i++) {
            for (int j = v[i]; j <= m; j++) {
                f[j] += f[j - v[i]];
            }
        }

        System.out.println(f[m]);
    }
}
```

