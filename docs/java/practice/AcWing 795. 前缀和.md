[795. 前缀和](https://www.acwing.com/problem/content/797/)

#### 算法：

*#前缀和*

#### 时间复杂度分析：

预处理前缀和需要遍历一遍数组，时间复杂度为 O(n)。

#### 代码：

```java
import java.util.*;

public class Main {
    private static final int N = 100010;
    private static int[] a = new int[N], s = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            a[i] = sc.nextInt();
            s[i] = s[i - 1] + a[i];
        }
        
        while (m-- > 0) {
            int l = sc.nextInt(), r = sc.nextInt();
            System.out.println(s[r] - s[l - 1]);
        }
    }
}
```

