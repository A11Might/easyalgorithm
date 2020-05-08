[826. 单链表](https://www.acwing.com/problem/content/828/)

#### 算法：

*#单链表*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    
    // head 表示头结点的下标，e[i] 表示节点i的值，ne[i] 表示节点i的next指针是多少，idx 存储当前已经用到了哪个点
    static int head, idx;
    static int[] e = new int[N], ne = new int[N];
    
    // 初始化链表
    static void init() {
        head = -1;
        idx = 0;
    }
    
    // 将 x 插到头结点
    static void addToHead(int x) {
        e[idx] = x;
        ne[idx] = head;
        head = idx++;
    }
    
    // 将 x 插到下标是 k 的点后面
    static void add(int k, int x) {
        e[idx] = x;
        ne[idx] = ne[k];
        ne[k] = idx++;
    }
    
    // 将下标是 k 的点后面的点删掉
    static void remove(int k) {
        ne[k] = ne[ne[k]];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        init();
        int n = sc.nextInt();
        while (n-- > 0) {
            int k, x;
            String op = sc.next();
            if (op.equals("H")) {
                x = sc.nextInt();
                addToHead(x);
            } else if (op.equals("I")) {
                k = sc.nextInt();
                x = sc.nextInt();
                // 由于链表元素是从 0 开始的，所以第 k 个元素对应下标为 k - 1
                add(k - 1, x);
            } else {
                k = sc.nextInt();
                if (k == 0) head = ne[head];
                else remove(k - 1);
            }
        }
        
        for (int i = head; i != -1; i = ne[i]) System.out.print(e[i] + " ");
    }
}
```

