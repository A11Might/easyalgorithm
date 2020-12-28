[798. 差分矩阵](https://www.acwing.com/problem/content/description/800/)

#### 算法：

*#差分*

#### 时间复杂度分析：

插入操作的时间复杂度为 O(1)。

#### 代码：

```java
import java.util.*;
import java.io.*;

class Main {
    static final int N = 1010;
    static int[][] a = new int[N][N], b = new int[N][N];
    
    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = sc.nextInt(), m = sc.nextInt(), q = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                a[i][j] = sc.nextInt();
                insert(i, j, i, j, a[i][j]); // 构建差分矩阵 b
            }
        }
        
        while (q-- > 0) {
            int x1 = sc.nextInt(), y1 = sc.nextInt(), x2 = sc.nextInt(), y2 = sc.nextInt(), c = sc.nextInt();
            insert(x1, y1, x2, y2, c);
        }
        
        // 求差分矩阵 b 的前缀和 a
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                a[i][j] = a[i - 1][j] + a[i][j - 1] - a[i - 1][j - 1] + b[i][j];
                out.write(a[i][j] + " ");
            }
            out.write("\n");
        }
        
        // 使用 BufferedWriter 打印，直接使用 System.out 会超时
        out.flush();
    }
    
    static void insert(int x1, int y1, int x2, int y2, int c) {
        b[x1][y1] += c;
        b[x2 + 1][y1] -= c;
        b[x1][y2 + 1] -= c;
        b[x2 + 1][y2 + 1] += c;
    }
}
```

