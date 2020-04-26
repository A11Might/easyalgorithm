[91. 最短Hamilton路径](https://www.acwing.com/problem/content/93/)

#### 算法：

*#DP#状态压缩DP*

**状态表示 - f(i, j)**

- 集合：所有从 0 走到 j，且走过的所有点是 i 的路径。

  其中 i 是二进制数，表示走过哪些城市。

- 属性：Min

**状态计算 - 集合划分**

枚举倒数第二个经过的点来划分 f(i, j) 表示的集合：

- 倒数第二个经过的点是 0：

- 倒数第二个经过的点是 1：

  ...

- 倒数第二个经过的点是 k：从 0 走到 k，再从 k 走到 j，且走到的所有点是 i。

  从 k 走到 j 是题目给出的，我们所有可以先考虑从 0 走到 k，且走过的所有点是 i 除去 j 的路径的最小值，然后在加上 k 到 j 的距离，f(i - {j}, k) + a(k , j)。

综上：f(i, j) = min(f(i - {j}, k) + a(k , j))。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 20, M = 1 << N;
    static int n;
    static int[][] w = new int[N][N];
    static int[][] f = new int[M][N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                w[i][j] = sc.nextInt();
            }
        }
        
        for (var arr : f) Arrays.fill(arr, 0x3f3f3f3f);
        f[1][0] = 0; // 起点 0 的状态
        
        for (int i = 0; i < 1 << n; i++) {
            for (int j = 0; j < n; j++) {
                // 只有 i 表示的状态经过 j 点时，状态 f(i, j) 才存在
                if ((i >> j & 1) == 1) {
                    for (int k = 0; k < n; k++) {
                        // 只有 i 表示的状态经过 k 点时，状态 f(i - {j}, k) 才存在
                        if ((i >> k & 1) == 1) {
                            f[i][j] = Math.min(f[i][j], f[i - (1 << j)][k] + w[k][j]);
                        }
                    }
                }
            }
        }
        
        System.out.println(f[(1 << n) - 1][n - 1]);
    }
}
```

