[799. 最长连续不重复子序列](https://www.acwing.com/problem/content/801/)

#### 算法：

*#双指针*

**朴素做法**

使用两个指针来枚举所有子序列，从中选取符合题意的最大值。

```java
int ret = 0;
for (int i = 0; i < n; i++) { // 固定右端点
    for (int j = 0; j <= j; j++) { // 枚举左端点 
        if (check(j, i)) ret = Math.max(ret, i - j + 1);
    }
}
```

**双指针**

观察发现，随着右端点向右移动，左端点只会向右移动的。因为如果左端点向左移动，则说明之前计算的最长子序列是错误的，之前计算的最长序列长度应加上向左移动的这一位。

因此我们只用枚举 i，再通过判断子序列中是否有重复元素来移动 j。

#### 时间复杂度分析：

瓶颈是最内层 whie 循环的执行次数，while 循环每执行一次 j 都会加 1，j 不会减少，所以最多只能执行 n 次。总时间复杂度为 O(n)。

#### 代码：

```java
import java.util.*;

public class Main {
    private static final int N = 100010;
    private static int[] q = new int[N], s = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        
        int ret = 0;
        for (int i = 0, j = 0; i < n; i++) {
            s[q[i]]++;
            // 维护区间 [j, i] 中没有重复元素
            while (s[q[i]] > 1) s[q[j++]]--;
            ret = Math.max(ret, i - j + 1);
        }
        
        System.out.println(ret);
    }
}
```

