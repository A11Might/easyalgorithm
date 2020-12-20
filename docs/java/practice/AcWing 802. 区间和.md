[802. 区间和](https://www.acwing.com/problem/content/804/)

#### 算法：

*#离散化*

操作和询问的坐标都是 10<sup>9</sup> 级别的，但操作数量只有 10<sup>5</sup> 级别。

我们求前缀和时，需要将坐标值当做下标来做，比如求坐标 [l, r] 之间的所有数字和，这样就需要开一个 10<sup>9</sup> 大小的数组，但数组并不能开出这么大，所以就可以使用离散化。

将所有需要用到的坐标放入数组中，排序、去重后离散化成从 1 开始的数，然后求前缀和。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;
import java.util.stream.Collectors;

public class Main {
    private static final int N = 300010;
    private static int[] a = new int[N], s = new int[N]; // 存储离散后的数和其前缀和
    private static List<Integer> alls = new ArrayList<>(); // 存储需要离散的数
    private static List<int[]> adds = new ArrayList<>(), querys = new ArrayList<>();
    
    private static int find(int x) {
        int l = 0, r = alls.size() - 1;
        while (l < r) {
            int mid = l + r >> 1;
            if (alls.get(mid) >= x) r = mid;
            else l = mid + 1;
        }
        
        return l + 1;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        while (n-- > 0) {
            int x = sc.nextInt(), c = sc.nextInt();
            adds.add(new int[] {x, c});
            alls.add(x); // 存储会用到的坐标
        }
        while (m-- > 0) {
            int l = sc.nextInt(), r = sc.nextInt();
            querys.add(new int[] {l, r});
            alls.add(l); // 存储会用到的坐标
            alls.add(r); // 存储会用到的坐标
        }
        
        // 离散化
        alls = alls.stream().sorted().distinct().collect(Collectors.toList());
        // 处理 + c 操作
        for (var add : adds) {
            int x = find(add[0]);
            a[x] += add[1];
        }
        // 处理 a 的前缀和
        for (int i = 1; i <= alls.size(); i++) s[i] = s[i - 1] + a[i];
        
        for (var query : querys) {
            int l = find(query[0]), r = find(query[1]);
            System.out.println(s[r] - s[l - 1]);
        }
    }
}
```

