[827. 双链表](https://www.acwing.com/problem/content/829/)

#### 算法：

*#双链表*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int idx;
    static int[] e = new int[N], l = new int[N], r = new int[N];
    
    // 初始化
    static void init() {
        // 0 是左端点，1 是右端点
        r[0] = 1;
        l[1] = 0;
        idx = 2;
    }
    
    // 在节点 a 的右边插入一个数 x
    static void insert(int a, int x) {
        e[idx] = x;
        r[idx] = r[a];
        l[idx] = a;
        l[r[a]] = idx;
        r[a] = idx++;
    }
    
    // 删除节点 a
    static void remove(int a) {
        r[l[a]] = r[a];
        l[r[a]] = l[a];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        init();
        int m = sc.nextInt();
        while (m-- > 0) {
            int k, x;
            String op = sc.next();
            if (op.equals("L")) {
                x = sc.nextInt();
                insert(0, x);
            } else if (op.equals("R")) {
                x = sc.nextInt();
                insert(l[1], x);
            } else if (op.equals("D")) {
                k = sc.nextInt();
                remove(k + 1);
            } else if (op.equals("IL")) {
                k = sc.nextInt();
                x = sc.nextInt();
                // 由于链表元素是从 2 开始的，所以第 k 个元素对应下标为 k + 1
                insert(l[k + 1], x);
            } else {
                k = sc.nextInt();
                x = sc.nextInt();
                insert(k + 1, x);
            }
        }
        
        for (int i = r[0]; i != 1; i = r[i]) System.out.print(e[i] + " ");
    }
}
```

