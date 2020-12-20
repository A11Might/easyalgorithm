[789. 数的范围](https://www.acwing.com/problem/content/791/)

#### 算法：

*#二分搜索*

#### 时间复杂度分析：

每次判断都会将数据规模减少一半，所以最多判断 logn 次，时间复杂度为 O(logn)。

#### 代码：

```java
import java.util.*;

public class Main {
    private static final int N = 100010;
    private static int[] q = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        
        while (m-- > 0) {
            int l = 0, r = n - 1, x = sc.nextInt();
            while (l < r) {
                int mid = l + r >> 1;
                // 寻找相同元素区间的第一个数，
                // 将区间划分为小于 x 和大于等于 x 两个部分。
                if (q[mid] >= x) r = mid;
                else l = mid + 1;
            }
            
            if (q[l] != x) System.out.println("-1 -1");
            else {
                System.out.print(l + " ");
                l = 0;
                r = n - 1;
                while (l < r) {
                    int mid = l + r + 1 >> 1;
                    // 寻找相同元素区间的最后一个数，
                    // 将区间分为小于等于 x 和大于 x 的两个部分
                    if (q[mid] <= x) l = mid;
                    else r = mid - 1;
                }
                System.out.println(l);
            }
        }
    }
}
```

