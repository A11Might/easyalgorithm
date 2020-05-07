[797. 差分](https://www.acwing.com/problem/content/799/)

#### 算法：

*#差分*

#### 时间复杂度分析：

插入操作的时间复杂度为 O(1)。

#### 代码：

```java
import java.util.*;

class Main {
    static int[] b;
    
    static void insert(int l, int r, int c) {
        b[l] += c;
        b[r + 1] -= c;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        int[] a = new int[n + 1];
        for (int i = 1; i <= n; i++) a[i] = sc.nextInt();
        
        // 差分序列
        b = new int[n + 2];
        for (int i = 1; i <= n; i++) insert(i, i, a[i]);
        
        // m 次区间加 c 操作
        while (m-- > 0) {
            int l = sc.nextInt(), r = sc.nextInt(), c = sc.nextInt();
            insert(l, r, c);
        }
        
        // 求 b 的前缀和 
        for (int i = 1; i <= n; i++) {
            a[i] = a[i - 1] + b[i];
            System.out.print(a[i] + " ");
        }
    }
}
```

