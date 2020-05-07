[795. 前缀和](https://www.acwing.com/problem/content/797/)

#### 算法：

*#前缀和*

#### 时间复杂度分析：

预处理前缀和需要遍历一遍数组，时间复杂度为 O(n)。

#### 代码：

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), q = sc.nextInt();
        int[] a = new int[n + 1];
        for (int i = 1; i <= n; i++) a[i] = sc.nextInt();
        
        // 也可以直接在 a 数组中求前缀和
        int[] s = new int[n + 1];
        for (int i = 1; i <= n; i++) s[i] = s[i - 1] + a[i]; // 前缀和的初始化
        
        while (q-- > 0) {
            int l = sc.nextInt(), r = sc.nextInt();
            System.out.println(s[r] - s[l - 1]); // 区间和的计算
        }
    }
}
```

