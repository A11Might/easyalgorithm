[2816. 判断子序列](https://www.acwing.com/problem/content/2818/)

#### 算法

*#双指针*

找单调性来优化暴力解（O(n * m)）

#### 时间复杂度分析：

双指针只会扫描一遍两数组，所以时间复杂度为 O(n + m)。

#### 代码：

```java
import java.util.*;

public class Main {
    private static final int N = 100010;
    private static int[] a = new int[N], b = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        for (int i = 0; i < n; i++) a[i] = sc.nextInt();
        for (int i = 0; i < m; i++) b[i] = sc.nextInt();
        
        int i = 0, j = 0;
        while (i < n && j < m) {
            if (a[i] == b[j]) i++;
            j++;
        }
        
        if (i == n) System.out.println("Yes");
        else System.out.println("No");
    }
}
```

```java
import java.util.*;

public class Main {
    private static final int N = 100010;
    private static int[] a = new int[N], b = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        for (int i = 0; i < n; i++) a[i] = sc.nextInt();
        for (int i = 0; i < m; i++) b[i] = sc.nextInt();
        
        int i = 0, j = 0;
        for (; i < n; i++, j++) {
            while (j < m && a[i] != b[j]) j++;
            if (j == m) {
                System.out.println("No");
                return;
            }
        }
        
        if (i == n) System.out.println("Yes");
    }
}
```


