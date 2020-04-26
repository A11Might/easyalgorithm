[898. 数字三角形](https://www.acwing.com/problem/content/900/)

#### 算法：

*#DP#线性DP*

**状态表示 - f(i, j)**

- 集合：所有从起点走到 (i, j) 的路径。
- 属性：Max

**状态计算 - 集合划分**

通过路径方向将 f(i, j) 表示的集合划分为：

- 来自左上方：f(i - 1, j - 1) + a[i, j]。
- 来自右上方：f(i - 1, j) + a[i, j]。

![ac898](5-1.png)

综上：f(i, j) = max(f(i - 1, j - 1) + a[i, j], f(i - 1, j) + a[i, j])。

注：每一行的两边都需要多初始化一个位置，计算最左侧或者最右侧位置的最大值会用到。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 510;
    static int n;
    static int[][] h = new int[N][N];
    static int[][] f = new int[N][N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                h[i][j] = sc.nextInt();
            }
        }
        
        for (var arr : f) Arrays.fill(arr, Integer.MIN_VALUE);
        f[1][1] = h[1][1];
        for (int i = 2; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                f[i][j] = Math.max(f[i - 1][j - 1], f[i - 1][j]) + h[i][j];
            }
        }
        
        int ret = Integer.MIN_VALUE;
        for (int i = 1; i <= n; i++) ret = Math.max(ret, f[n][i]);
        System.out.println(ret);
    }
}
```

