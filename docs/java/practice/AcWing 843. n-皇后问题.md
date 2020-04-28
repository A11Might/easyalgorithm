[843. n-皇后问题](https://www.acwing.com/problem/content/description/845/)

#### 算法：

*#dfs#暴搜*

依次枚举每个位置上是否放置皇后。

#### 时间复杂度分析：

时间复杂度为 O(2<sup>n <sup>2</sup></sup>)。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 10;
    static int n;
    static char[][] h = new char[N][N];
    static boolean[] row = new boolean[N], col = new boolean[N], dia1 = new boolean[2 * N], dia2 = new boolean[2 * N];
    
    static void dfs(int x, int y, int cnt) {
        if (y == n) {
            x++;
            y = 0;
        }
        if (x == n) {
            if (cnt == n) {
                for (int i = 0; i < n; i++) {
                    for (int j = 0; j < n; j++) System.out.print(h[i][j]);
                    System.out.println();
                }
                System.out.println();
            }
            return;
        }
        
        // 枚举当前位置上是否放置皇后
        // 在当前位置不放入皇后
        h[x][y] = '.';
        dfs(x, y + 1, cnt);
        
        // 在当前位置放入皇后
        if (row[x] || col[y] || dia1[x + y] || dia2[x - y + n]) return;
        row[x] = col[y] = dia1[x + y] = dia2[x - y + n] = true;
        h[x][y] = 'Q';
        dfs(x, y + 1, cnt + 1);
        row[x] = col[y] = dia1[x + y] = dia2[x - y + n] = false;
        h[x][y] = '.';
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        
        dfs(0, 0, 0);
    }
}
```

