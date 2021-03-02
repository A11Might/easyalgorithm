[1024. 装箱问题](https://www.acwing.com/problem/content/1026/)

#### 算法：

*DP* *背包问题*

**简化问题**

将每个物品的体积看成体积的同时也看成价值，因此转化成 01 背包问题求得的结果，就是在体积不超过总体积的情况下，价值最大是多少。

也就是：在体积不超过总体积的情况下，体积最大是多少（对应总体积剩余最少）。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 20010;
    static int n, m;
    static int[] f = new int[N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        m = sc.nextInt();
        n = sc.nextInt();

        for (int i = 1; i <= n; i++) {
            int v = sc.nextInt();
            for (int j = m; j >= v; j--) {
                f[j] = Math.max(f[j], f[j - v] + v);
            }
        }

        System.out.println(m - f[m]);
    }
}
```

