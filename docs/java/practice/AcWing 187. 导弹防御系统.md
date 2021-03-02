[187. 导弹防御系统](https://www.acwing.com/problem/content/189/)

#### 算法：

*DP* *LIS* *贪心* *DFS*

从前往后遍历每个数，对于每个数：

- 将其放入下降子序列（记录每个序列的结尾的数组是 `单调递增` 的）

  - 如果现有子序列的结尾都小于当前数，则创建新子序列；

  - 如果现有子序列的结尾有大于等于当前数的，则将当前数放到结尾大于等于它的最小子序列后面。

    基于贪心：当前数放完后一定会在一个子序列的末尾，那么剩余的其他子序列的结尾一定是越大越好，因此我们应该让当前数替代一个较小的子序列的结尾。

- 将其放入上升子序列（记录每个序列的结尾的数组是 `单调递减` 的）

  - 如果现有子序列的结尾都大于当前数，则创建新子序列；
  
  - 如果现有子序列的结尾有小于等于当前数的，则将当前数放到结尾小于等于它的最大子序列后面。
  
    基于贪心：当前数放完后一定会在一个子序列的末尾，那么剩余的其他子序列的结尾一定是越小越好，因此我们应该让当前数替代一个较大的子序列的结尾。

因为我们无法确定要将每个数放到那个序列中，所以使用爆搜。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 55;
    static int n;
    static int[] h = new int[N];
    static int[] up = new int[N], down = new int[N]; // up 数组表示所有严格上升子序列的结尾，down 数组表示所有严格下降子序列的结尾
    static int ans;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        while (n != 0) {
            for (int i = 0; i < n; i++) h[i] = sc.nextInt();

            ans = n;
            dfs(0, 0, 0);
            System.out.println(ans);

            n = sc.nextInt();
        }
    }
 
    static void dfs(int u, int su, int sd) { // su 表示严格上升子序列的个数，sd 表示严格下降子序列的个数
        if (su + sd >= ans) return;
        if (u == n) {
            ans = su + sd;
            return;
        }

        // 将 u 放入下降子序列
        int k = 0;
        while (k < sd && down[k] <= h[u]) k++;
        if (k < sd) {
            int t = down[k];
            down[k] = h[u];
            dfs(u + 1, su, sd);
            down[k] = t; // 恢复现场
        } else {
            down[k] = h[u];
            dfs(u + 1, su, sd + 1);
            // k == sd 时，没有恢复现场，是因为有 sd 记录长度，不需要恢复现场。
        }

        // 将 u 放入上升子序列
        k = 0;
        while (k < su && up[k] >= h[u]) k++;
        if (k < su) {
            int t = up[k];
            up[k] = h[u];
            dfs(u + 1, su, sd);
            up[k] = t; // 恢复现场
        } else {
            up[k] = h[u];
            dfs(u + 1, su + 1, sd);
            // k == su 时，没有恢复现场，是因为有 su 记录长度，不需要恢复现场。
        }
    }
}
```

