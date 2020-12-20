[790. 数的三次方根](https://www.acwing.com/problem/content/792/)

#### 算法：

*#二分搜索*

#### 时间复杂度分析：

每次判断都会将数据规模减少一半，所以最多判断 logn 次，时间复杂度为 O(logn)。

#### 代码：

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        double n = sc.nextDouble();
        double l = -100, r = 100;
        // 精度的经验值是题目要求 +2
        while (r - l > 1e-8) {
            double mid = (l + r) / 2;
            if (mid * mid * mid >= n) r = mid;
            else l = mid;
        }
        
        System.out.printf("%.6f\n",l);
    }
}
```

