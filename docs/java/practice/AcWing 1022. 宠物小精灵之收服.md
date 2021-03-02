[1022. 宠物小精灵之收服](https://www.acwing.com/problem/content/1024/)

#### 算法：

*DP* *背包问题*

**简化问题**

- 花费 1：精灵球数量；花费 2：皮卡丘体力值

- 价值：小精灵的数量

**状态表示 - f(i, j, k)**

- 集合：所有只从前 i 个物品中选，且花费 1 不超过 j，花费 2 不超过 k 的选法

- 属性：Max

**状态计算 - 集合划分**

以是否选择第 i 个物品来划分 f(i, j, k) 表示的集合：

- 不选第 i 个物品：f(i - 1, j, k)

- 选第 i 个物品：f(i - 1, j - v1[i], k - v2[i]) + 1

综上：

- 最多收服的小精灵数量：f(K, N, M)

- 最少耗费体力怎么计算：从小到大看最小的 f(K, N, m) == f(K, N, M) 是多少


#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010, M = 510;
    static int n, V1, V2;
    static int[][] f = new int[N][M];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        V1 = sc.nextInt();
        V2 = sc.nextInt();
        n = sc.nextInt();

        for (int i = 1; i <= n; i++) {
            int v1 = sc.nextInt(), v2 = sc.nextInt();
            for (int j = V1; j >= v1; j--) {
                for (int k = V2 - 1; k >= v2; k--) { // 皮卡丘的体力必须大于 0
                    f[j][k] = Math.max(f[j][k], f[j - v1][k - v2] + 1);
                }
            }
        }      

        int k = V2 - 1;
        while (k > 0 && f[V1][k - 1] == f[V1][V2 - 1]) k--;
        System.out.println(f[V1][V2 - 1] + " " + (V2 - k));
    }
}
```

