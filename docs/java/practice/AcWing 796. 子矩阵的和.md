[796. 子矩阵的和](https://www.acwing.com/problem/content/798/)

#### 算法：

*#前缀和*

#### 时间复杂度分析：

预处理前缀和需要遍历一遍矩阵，时间复杂度为 O(n * m)。

#### 代码：

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt(), q = sc.nextInt();
        int[][] a = new int[n + 1][m + 1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                a[i][j] = sc.nextInt();
            }
        }
        
        // 也可以直接在 a 矩阵中求前缀和
        int[][] s = new int[n + 1][m + 1];
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + a[i][j]; // 二维前缀和的初始化
            }
        }
        
        while (q-- > 0) {
            int x1 = sc.nextInt(), y1 = sc.nextInt(), x2 = sc.nextInt(), y2 = sc.nextInt();
            System.out.println(s[x2][y2] - s[x2][y1 - 1] - s[x1 - 1][y2] + s[x1 - 1][y1 - 1]); // 子矩阵和的计算
        }
    }
}
```

