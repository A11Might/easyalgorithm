[907. 区间覆盖](https://www.acwing.com/problem/content/909/)

#### 算法：

*#贪心*

1. 将区间按照左端点从小到大排序。
2. 从前往后依次枚举每个区间，在所有能覆盖 s 的区间中，选择右端点最大的区间，然后将 s 更新为该区间的右端点。

**证明**

假设如上算法得到的可行解的区间数是 cnt，最优解（最少区间数）是 ans。

我们寻找两组区间中第一个不同的区间 a, b：

- 这两个不同的区间 a，b 的左端点都与前一个区间（是相同的）相交。
- 如上算法得到的可行解的区间 a 的右端点是最大的，也就是说它一定大于最优解中对应的区间 b 的右端点。
- 综上，我们可以使用可行解中的区间 a 替换最优解中的区间 b，并且这个操作对方案中的区间数是没有影响的。

然后我们依次对其余不同的区间进行替换，最终可行解 cnt 和 最优解 ans 变得完全相同，可以得到 ans = cnt。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int s, t, n;
    static int[][] range = new int[N][2];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        s = sc.nextInt();
        t = sc.nextInt();
        n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            range[i][0] = sc.nextInt();
            range[i][1] = sc.nextInt();
        }
        
        Arrays.sort(range, 0, n, (o1, o2) -> o1[0] - o2[0]);
        int ret = 0;
        for (int i = 0; i < n; i++) {
            int j = i, r = (int) -2e9;
            while (j < n && range[j][0] <= s) {
                r = Math.max(r, range[j][1]);
                j++;
            }
            
            if (r < s) {
                System.out.println("-1");
                return;
            }
            
            ret++;
            s = r;
            i = j - 1;
            
            if (r >= t) {
                System.out.println(ret);
                return;
            }
        }
        
        System.out.println("-1");
    }
}
```

