[896. 最长上升子序列 II](https://www.acwing.com/problem/content/898/)

#### 算法：

*#DP#线性DP*

最长上升子序列朴素做法的时间复杂度是 O(n<sup>2</sup>)，等于 100 亿，一定会超时，所以需要优化。

**优化**

使用一个数组 q 记录不同长度的上升子序列的尾数的最小值。

数组 q 一定是单调递增的？

反证法：假设数组 q 不是单调递增的，存在 q(5) >= q(6)，其中 q(5), q(6) 分别对应长度为 5 和 6 的上升子序列的尾数的最小值 a, b，那么在长度为 6 的子序列中一定存在一个长度为 5 且尾数 c 小于 b 的上升子序列，由 b <= a 可得 c <= a，也就是说存在一个长度为 5 的上升子序列的尾数小于 q(5)，矛盾了，所以 q 一定是单调递增的。

<img src="896.png" style="zoom:50%;" />

遍历原始数组中的元素，通过二分搜索将当前遍历到的元素 a 插入数组 q 中最大的、尾数小于 a 的上升子序列 q[i] 后面，构成长度 +1 的新上升子序列（元素 q[i +1] 一定大于或者等于 a，所以可以使用 a 进行更新）。最终，返回最长上升子序列的长度。

#### 时间复杂度分析：

遍历的数组长度为 n，每次遍历二分的时间复杂度为 logn，所以总时间复杂度是 O(n * logn)，50 万，不会超时。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int n;
    static int[] h = new int[N];
    static int[] q = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        for (int i = 0; i < n; i++) h[i] = sc.nextInt();
        
        int len = 0; // 当前最长上升子序列的长度，也就是数组 q 的长度
        for (int i = 0; i < n; i++) {
            int l = 0, r = len;
            while (l < r) {
                int mid = l + r + 1 >> 1;
                if (q[mid] < h[i]) l = mid;
                else r = mid - 1;
            }
            len = Math.max(len, r + 1);
            q[r + 1] = h[i];
        }
        
        System.out.println(len);
    }
}
```



