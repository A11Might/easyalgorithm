[899. 编辑距离](https://www.acwing.com/problem/content/901/)

#### 算法：

*#DP#线性DP*

同最短编辑距离

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int n, m;
    static char[][] strs = new char[N][20];
    static int[][] f = new int[N][N];
    
    static int editDistance(char[] a, char[] b) {
        int la = a.length - 1, lb = b.length - 1;
        for (int i = 0; i <= la; i++) f[i][0] = i;
        for (int j = 0; j <= lb; j++) f[0][j] = j;
        
        for (int i = 1; i <= la; i++) {
            for (int j = 1; j <= lb; j++) {
                if (a[i] == b[j]) f[i][j] = f[i -1][j - 1];
                else f[i][j] = Math.min(f[i - 1][j - 1], Math.min(f[i - 1][j], f[i][j - 1])) + 1;
            }
        }
        
        return f[la][lb];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        for (int i = 0; i < n; i++) {
            strs[i] = (" " + sc.next()).toCharArray();
        }
        
        while (m-- > 0) {
            int ret = 0;
            char[] b = (" " + sc.next()).toCharArray();
            int limit = sc.nextInt();
            for (int i = 0; i < n; i++) {
                if (editDistance(strs[i], b) <= limit) ret++;
            }
            System.out.println(ret);
        }
    }
}
```

