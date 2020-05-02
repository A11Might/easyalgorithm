[905. 区间选点](https://www.acwing.com/problem/content/907/)

#### 算法：

*#贪心*

1. 将每个区间按右端点从小到大排序。
2. 从前往后依次枚举每个区间：
   - 如果当前区间已经包含点，则直接跳过。
   - 否则，选择当前区间的右端点（贪心，选择局部最优解来试图得到全局最优解）。

**证明**

- 如上算法，可以保证每个区间都包含一个点，是一个可行解记作 cnt。假设最优解（选择的点的最小数量）是 ans，可得 ans <= cnt。

- 算法过程中，如果当前区间已经包含点，则直接跳过。所以 cnt 个点，分别对应 cnt 个不相交的区间，但还有若干相交的区间，所以最优解 ans >= cnt。
- 可以推出 ans = cnt。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int n;
    static int[][] range = new int[N][2];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        
        for (int i = 0; i < n; i++) {
            range[i][0] = sc.nextInt();
            range[i][1] = sc.nextInt();
        }
        
        Arrays.sort(range, 0, n, (o1, o2) -> o1[1] - o2[1]);
        
        int ret = 0, ed = (int) -2e9;
        for (int i = 0; i < n; i++) {
            if (range[i][0] > ed) {
                ret++;
                ed = range[i][1];
            }
        }
        
        System.out.println(ret);
    }
}
```

