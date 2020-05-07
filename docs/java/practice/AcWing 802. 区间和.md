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

class Main {
    static List<Integer> a;

    static int find(int x) {
        int l = 0, r = a.size() - 1;
        while (l < r) {
            int mid = l + r >> 1;
            if (a.get(mid) >= x) r = mid;
            else l = mid + 1;
        }
        return r + 1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        a = new ArrayList<>(); // 存储需要离散的数

        List<int[]> add = new ArrayList<>(); // 存储加 c 操作
        for (int i = 0; i < n; i++) {
            int x = sc.nextInt(), c = sc.nextInt();
            add.add(new int[] {x, c});
            a.add(x); // 存储会用到的坐标
        }

        List<int[]> query = new ArrayList<>(); // 存储查询操作
        for (int i = 0; i < m; i++) {
            int l = sc.nextInt(), r = sc.nextInt();
            query.add(new int[] {l, r});
            a.add(l); // 存储会用到的坐标
            a.add(r); // 存储会用到的坐标
        }

        // 离散
        a = a.stream().sorted().distinct().collect(Collectors.toList());

        // 处理加 c 操作
        int[] b = new int[a.size() + 1]; // 存储离散后的数
        for (int[] arr : add) {
            int x = find(arr[0]);
            b[x] += arr[1];
        }

        // 预处理前缀和
        int[] s = new int[a.size() + 1];
        for (int i = 1; i <= a.size(); i++) s[i] = s[i - 1] + b[i];

        // 处理询问
        for (int[] arr : query) {
            int l = find(arr[0]), r = find(arr[1]);
            System.out.println(s[r] - s[l - 1]);
        }
    }
}
```

