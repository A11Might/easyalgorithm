[787. 归并排序](https://www.acwing.com/problem/content/789/)

#### 算法：

*#归并排序*

#### 时间复杂度分析：

根据递归树分析：

1. 每次递归是将数组等分为两个部分，再递归解决两个这两个部分，也就是说递归树高度的期望是 logn。
2. 递归树每层都需要遍历整个数组，时间复杂度是 O(n)。

所以总的平均时间复杂度是 O(n * logn)。

#### 代码：

```java
import java.util.*;

public class Main {
    private static final int N = 100010;
    private static int[] q = new int[N], t = new int[N];
    
    private static void mergeSort(int[] q, int l, int r) {
        if (l >= r) return;
        
        int mid = l + r >> 1;
        mergeSort(q, l, mid);
        mergeSort(q, mid + 1, r);
        
        int i = l, j = mid + 1, k = l;
        while (i <= mid && j <= r) {
            if (q[i] <= q[j]) t[k++] = q[i++];
            else t[k++] = q[j++];
        }
        while (i <= mid) t[k++] = q[i++];
        while (j <= r) t[k++] = q[j++];
        
        for (i = l; i <= r; i++) q[i] = t[i];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) q[i] = sc.nextInt();
        mergeSort(q, 0, n - 1);
        for (int i = 0; i < n; i++) System.out.print(q[i] + " ");
    }
}
```

