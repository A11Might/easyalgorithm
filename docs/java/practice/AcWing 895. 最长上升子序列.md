[895. 最长上升子序列](https://www.acwing.com/problem/content/897/)

#### 算法：

*#DP#线性DP*

**状态表示 - f(i)**

- 集合：所有以第 i 个元素结尾的上升子序列。
- 属性：Max

**状态计算 - 集合划分**

枚举第 i 个元素的前一个元素来划分 f(i) 表示的集合：

- 第 i 个元素的前没有元素

- 第 i 个元素的前一个元素是 s[1]

  ...

- 第 i 个元素的前一个元素是 s[i - 1]

只有当第 i 个元素的前一个元素小于第 i 个元素时，对应的那一类才存在，所以我们在所有存在的情况中取一个最大值：f(i) = max(f(j) + 1)，j ∈ [0, i - 1]。

#### 时间复杂度分析：

状态数量为 n，转移的数量也是 n，所以总时间复杂度是 O(n<sup>2</sup>)。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int n;
    static int[] h = new int[N];
    static int[] f = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        for (int i = 1; i <= n; i++) h[i] = sc.nextInt();
        
        for (int i = 1; i <= n; i++) {
            f[i] = 1;
            for (int j = 1; j < i; j++) {
                if (h[i] > h[j]) f[i] = Math.max(f[i], f[j] + 1);
            }
        }
        
        int ret = 0;
        for (int i = 1; i <= n; i++) ret = Math.max(ret, f[i]);
        System.out.println(ret);
    }
}
```

