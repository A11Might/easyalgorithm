[148. 合并果子](https://www.acwing.com/problem/content/150/)

#### 算法：

*#贪心*

每次合并两个最小的点。

**证明**

Huffman 树

![](148.png)

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        
        PriorityQueue<Integer> heap = new PriorityQueue<>((o1, o2) -> o1 - o2);
        while (n-- > 0) {
            int a = sc.nextInt();
            heap.offer(a);
        }
        
        int ret = 0;
        while (heap.size() > 1) {
            int a = heap.poll(), b = heap.poll();
            ret += a + b;
            heap.offer(a + b);
        }
        
        System.out.println(ret);
    }
}
```

