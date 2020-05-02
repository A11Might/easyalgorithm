[913. 排队打水](https://www.acwing.com/problem/content/description/915/)

#### 算法：

*#贪心*

按照从小到大的顺序排队，总时间最小。

**证明**

调整法：假设最优解（等待时间之和最小）不是从小到大排序的，则一定存在 a<sub>i</sub> > a<sub>i +1</sub>，我们交换一下他们的顺序。

因为排队打水的等待时间是：a<sub>1</sub> * (n - 1) + a<sub>2</sub> * (n - 2) + ... + a<sub>n - 1</sub>，所以交换对其他人是没有影响的，所以我们只考虑交换的这两个人。

a<sub>i</sub> * (n - i) + a<sub>i + 1</sub> * (n - i - 1)，交换前

a<sub>i + 1</sub> * (n - i) + a<sub>i </sub> * (n - i - 1)，交换后

a<sub>i</sub> * (n - i) + a<sub>i + 1</sub> * (n - i - 1) - a<sub>i + 1</sub> * (n - i) + a<sub>i </sub> * (n - i - 1) = a<sub>i</sub> - a<sub>i + 1</sub> > 0

所以可以得到交换后的等待时间更小，矛盾了，假设不成立。

#### 时间复杂度分析：



#### 代码：

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
        
        long ret = 0;
        for (int i = 0; i < n; i++) ret += h[i] * (n - i - 1);
        
        System.out.println(ret);
    } 
}
```

