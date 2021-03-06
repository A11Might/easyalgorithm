[154. 滑动窗口](https://www.acwing.com/problem/content/156/)

#### 算法：

*#滑动窗口*

同双指针算法一样，先想一下朴素算法，再挖掘一些性质，将目光集中在较少的状态上，从而将时间复杂度降低。

**朴素算法**

使用队列维护一个大小为 k 个窗口，每次从头到尾遍历队列来寻找窗口中最小值。

**优化**

当队列中的元素 ax >= ay 并且 x < y 时，ax 永远不会作为答案输出。因为 ay 不仅不 ax 小，而且 ay 会晚于 ax 出队，所以只要存在 ay，ax 永远不会作为答案输出。

如果我们删除队列中所有逆序对中较大的元素，队列中剩余的元素就是单调递增的，所以队列中的最小值就是队首元素，这样每次求窗口中的最小值时，直接返回队首就可以了。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;
import java.io.*;

class Main {
    static final int N = 1000010;
    static int hh, tt;
    static int[] q = new int[N];

    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
        int n = sc.nextInt(), k = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();

        hh = 0;
        tt = -1;
        for (int i = 0; i < n; i++) {
            if (hh <= tt && q[hh] < i - k + 1) hh++;
            while (hh <= tt && nums[i] <= nums[q[tt]]) tt--;
            q[++tt] = i;
            if (i >= k - 1) out.write(nums[q[hh]] + " ");
        }    

        out.write("\n");
        hh = 0;
        tt = -1;
        for (int i = 0; i < n; i++) {
            if (hh <= tt && q[hh] < i - k + 1) hh++;
            while (hh <= tt && nums[i] >= nums[q[tt]]) tt--;
            q[++tt] = i;
            if (i >= k - 1) out.write(nums[q[hh]] + " ");
        }

        // 使用 BufferedWriter 打印，直接使用 System.out 会超时
        out.flush();
    }
}
```

