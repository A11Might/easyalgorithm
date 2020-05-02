[104. 货仓选址](https://www.acwing.com/problem/content/106/)

#### 算法：

*#贪心*

货仓建在中位数的位置上

**证明**

假设货仓建设位置为 x，则货仓到每家商店的距离之和就是 |x<sub>1</sub> - x| + |x<sub>2</sub> - x| + ... + |x<sub>n - 1</sub> - x| + |x<sub>n</sub> - x|。

我们两两考虑其中的项，|x<sub>1</sub> - x| + |x<sub>n</sub> - x| + |x<sub>2</sub> - x| + |x<sub>n - 1</sub> - x| + ...。

|x<sub>1</sub> - x| + |x<sub>n</sub> - x| 表示的就是 x 到 x<sub>1</sub> 和 x<sub>n</sub> 的距离，若x 位于 [x<sub>1</sub>, x<sub>n</sub>] 外面的话，|x<sub>1</sub> - x| + |x<sub>n</sub> - x| 的值大于 |x<sub>1</sub> - x<sub>n</sub>|；若 x 位于 [x<sub>1</sub>, x<sub>n</sub>] 之间的话，|x<sub>1</sub> - x| + |x<sub>n</sub> - x| 的值等于 |x<sub>1</sub> - x<sub>n</sub>|。所以可以得到 |x<sub>1</sub> - x| + |x<sub>n</sub> - x| >= |x<sub>1</sub> - x<sub>n</sub>|。

每一个都可以如上分析：|x<sub>1</sub> - x| + |x<sub>n</sub> - x| + |x<sub>2</sub> - x| + |x<sub>n - 1</sub> - x| + ... >= |x<sub>1</sub> - x<sub>n</sub>| + |x<sub>2</sub> - x<sub>n</sub>| + ...

当我们将 x 选为每两个数之间的数 - 所有数的中位数，就可以取到最小值。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int n;
    static int[] h = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        for (int i = 0; i < n; i++) h[i] = sc.nextInt();
        
        Arrays.sort(h, 0, n);
        
        int ret = 0;
        for (int i = 0; i < n; i++) ret += Math.abs(h[i] - h[n / 2]);
        System.out.println(ret);
    }
}
```

