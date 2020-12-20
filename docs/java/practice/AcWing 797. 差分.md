[797. 差分](https://www.acwing.com/problem/content/799/)

#### 算法：

*#差分*

#### 时间复杂度分析：

插入操作的时间复杂度为 O(1)。

#### 代码：

```java
import java.util.*;

public class Main {
    private static final int N = 100010;
    private static int[] a = new int[N], b = new int[N];
    
    private static void insert(int l, int r, int c) {
        b[l] += c;
        b[r + 1] -= c;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            a[i] = sc.nextInt();
            insert(i, i, a[i]); // 构建差分序列
        }
        
        while (m-- > 0) {
            int l = sc.nextInt(), r = sc.nextInt(), c = sc.nextInt();
            insert(l, r, c);
        }
        
        // 求差分序列 b 的前缀和 a
        for (int i = 1; i <= n; i++) {
            a[i] = a[i - 1] + b[i];
            System.out.print(a[i] + " ");
        }
    }
}
```

