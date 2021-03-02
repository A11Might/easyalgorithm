[1010. 拦截导弹](https://www.acwing.com/problem/content/1012/)

#### 算法：

*DP* *LIS* *贪心*

**贪心**

当前数放完后一定会在一个子序列的末尾，那么剩余的其他子序列的结尾一定是越大越好，因此我们应该让当前数替代一个较小的子序列的结尾。

**流程**

从前往后遍历每个数，对于每个数：

- 如果现有子序列的结尾都小于当前数，则创建新子序列；

- 如果现有子序列的结尾有大于等于当前数的，则将当前数放到结尾大于等于它的最小子序列后面。

这样记录每个序列的结尾的数组是单调递增的。

**拓展**

一个序列最少用多少个非上升子序列把它覆盖掉的方案数是等于这个序列的最长上升子序列的方案数的。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int n;
    static int[] h = new int[N];
    static int[] f = new int[N], q = new int[N]; // q 数组表示所有下降子序列的结尾

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] strs = sc.nextLine().split(" ");
        n = strs.length;
        for (int i = 0; i < n; i++) h[i] = Integer.valueOf(strs[i]);

        int ret = 0, cnt = 0; // ret 表示最多能拦截的导弹数，cnt 表示要拦截所有导弹最少要配备的系统数
        for (int i = 0; i < n; i++) {
            f[i] = 1;
            for (int j = 0; j < i; j++) {
                if (h[j] >= h[i]) f[i] = Math.max(f[i], f[j] + 1);
            }
            ret = Math.max(ret, f[i]);

            int k = 0;
            while (k < cnt && q[k] < h[i]) k++;
            if (k == cnt) q[cnt++] = h[i]; // 如果现有子序列的结尾都小于当前数，则创建新子序列
            else q[k] = h[i]; // 如果现有子序列的结尾有大于等于当前数的，则将当前数放到结尾大于等于它的最小子序列后面
        }

        System.out.printf("%d\n%d\n", ret, cnt);
    }
}
```

