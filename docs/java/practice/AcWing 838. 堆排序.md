[838. 堆排序](https://www.acwing.com/problem/content/840/)

#### 算法：

*#堆*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int size;
    static int[] h = new int[N];
    
    // 向下堆化
    static void down(int u) {
        int t = u;
        if (u * 2 <= size && h[t] > h[u * 2]) t = u * 2;
        if (u * 2 + 1 <= size && h[t] > h[u * 2 + 1]) t = u * 2 + 1;
        if (u != t) {
            int tmp = h[t];
            h[t] = h[u];
            h[u] = tmp;
            down(t);
        }
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        size = n;
        for (int i = 1; i <= n; i++) h[i] = sc.nextInt();
        
        // 建堆
        for (int i = n / 2; i > 0; i--) down(i);
        
        while (m-- > 0) {
            System.out.print(h[1] + " ");
            h[1] = h[size];
            size--;
            down(1);
        }
    }
}
```

