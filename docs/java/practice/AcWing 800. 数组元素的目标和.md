[800. 数组元素的目标和](https://www.acwing.com/problem/content/802/)

#### 算法

*#双指针*

找单调性来优化暴力解（O(n * m)）

由于序列 a 和 b 都是单调递增的，对于每一个 i，都找一个 j，使得 ai + bj >= x 并且 j 最小（最靠左的），这样就有单调性了：当 i 往后移动的过程中，j 一定往前移动。因为总和 x 是不变的，i 变大之后，j 只能减小。

#### 时间复杂度分析：

双指针只会扫描一遍两数组，所以时间复杂度为 O(n + m)。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int[] a = new int[N], b = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt(), x = sc.nextInt();
        for (int i = 0; i < n; i++) a[i] = sc.nextInt();
        for (int i = 0; i < m; i++) b[i] = sc.nextInt();
        
        for (int i = 0, j = m - 1; i < n; i++) {
            while (j >= 0 && a[i] + b[j] > x) j--;
            if (j >= 0 && a[i] + b[j] == x) System.out.println(i + " " + j);
        }
    }
}
```



