[AcWing 785. 快速排序](https://www.acwing.com/problem/content/description/787/)

#### 算法：

*#快速排序*

#### 时间复杂度分析：

根据递归树分析：

1. 每次递归的期望是将数组等分为左右两个部分，再递归解决这两个部分，也就是说递归树高度的期望是 logn。
2. 递归树每层都需要遍历整个数组，时间复杂度是 O(n)。

所以总的平均时间复杂度是 O(n * logn)。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int[] q = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        quickSort(q, 0, n - 1);
        for (int i = 0; i < n; i++) System.out.print(q[i] + " ");
    }
    
    static void quickSort(int[] q, int l, int r) {
        if (l >= r) return;
        
        int i = l - 1, j = r + 1, x = q[l + r >> 1];
        while (i < j) {
            do i++; while (q[i] < x);
            do j--; while (q[j] > x);
            if (i < j) {
                int t = q[j];
                q[j] = q[i];
                q[i] = t;
            }
        }
        
        quickSort(q, l, j);
        quickSort(q, j + 1, r);
    }
}
```

