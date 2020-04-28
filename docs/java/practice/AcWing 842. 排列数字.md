[842. 排列数字](https://www.acwing.com/problem/content/844/)

#### 算法：

*#dfs#暴搜*

依次枚举每个位置上填写的数字。

#### 时间复杂度分析：



#### 代码

```java
import java.util.*;

class Main {
    static final int N = 10;
    static int n;
    static int[] ret = new int[N];
    
    // 由于题目数据范围是 1 ≤ n ≤ 7，可以使用整型变量 st 代替布尔数组
    static void dfs(int u, int st) {
        if (u == n) {
            for (int i = 0; i < n; i++) System.out.print(ret[i] + " ");
            System.out.println();
            return;
        }
        // 枚举当前位置上填写的数字
        for (int i = 1; i <= n; i++) {
            if ((st >> i & 1) == 1) continue;
            ret[u] = i;
            dfs(u + 1, st + (1 << i));
        }
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        
        dfs(0, 0);
    }
}
```

