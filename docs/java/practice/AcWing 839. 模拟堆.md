[839. 模拟堆](https://www.acwing.com/problem/content/841/)

#### 算法：

*#堆*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int size;
    static int[] h = new int[N], ph = new int[N], hp = new int[N];
    
    static void swap(int[] arr, int a, int b) {
        int tmp = arr[b];
        arr[b] = arr[a];
        arr[a] = tmp;
    }
    
    static void heapSwap(int a, int b) {
        swap(ph, hp[a], hp[b]);
        swap(hp, a, b);
        swap(h, a, b);
    }
    
    static void down(int u) {
        int t = u;
        if (u * 2 <= size && h[u * 2] < h[t]) t = u * 2;
        if (u * 2 + 1 <= size && h[u * 2 + 1] < h[t]) t = u * 2 + 1;
        if (u != t) {
            heapSwap(u, t);
            down(t);
        }
    }
    
    static void up(int u) {
        while (u / 2 > 0 && h[u] < h[u / 2]) {
            heapSwap(u, u / 2);
            u >>= 1;
        }
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // m 用于标记当前插入的是第几个数
        int n = sc.nextInt(), m = 0;
        while (n-- > 0) {
            int k, x;
            String op = sc.next();
            if (op.equals("I")) {
                x = sc.nextInt();
                size++;
                m++;
                ph[m] = size;
                hp[size] = m;
                h[size] = x;
                up(size);
            } else if (op.equals("PM")) {
                System.out.println(h[1]);
            } else if (op.equals("DM")) {
                heapSwap(1, size--);
                down(1);
            } else if (op.equals("D")) {
                k = sc.nextInt();
                k = ph[k];
                heapSwap(k, size--);
                down(k);
                up(k);
            } else {
                k = sc.nextInt();
                x = sc.nextInt();
                k = ph[k];
                h[k] = x;
                down(k);
                up(k);
            }
        }
    }
}
```

