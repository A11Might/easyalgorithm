[423. 采药](https://www.acwing.com/problem/content/425/)

#### 算法：

*DP* *背包模型*

**简化问题**

把每个草药看成一个物品，时间看成体积，价值就是价值，就可以将题目转化为 01 背包问题。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int n, m;
    static int[] f = new int[N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        m = sc.nextInt();
        n = sc.nextInt();

        for (int i = 1; i <= n; i++) {
            int v = sc.nextInt(), w = sc.nextInt();
            for (int j = m; j >= v; j--) {
                f[j] = Math.max(f[j], f[j - v] + w);
            }
        }

        System.out.println(f[m]);
    }
}
```

