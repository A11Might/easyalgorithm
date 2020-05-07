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

class Main {
    static int n;
    static int[] nums, tmp;
    
    static void mergeSort(int[] nums, int l, int r) {
        if (l >= r) return;
        
        int mid = l + r >> 1;
        mergeSort(nums, l, mid);
        mergeSort(nums, mid + 1, r);
        
        int k = l, i = l, j = mid + 1;
        while (i <= mid && j <= r) {
            if (nums[i] <= nums[j]) tmp[k++] = nums[i++];
            else tmp[k++] = nums[j++];
        }
        while (i <= mid) tmp[k++] = nums[i++];
        while (j <= r) tmp[k++] = nums[j++];
        
        for (i = l; i <= r; i++) nums[i] = tmp[i];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        nums = new int[n];
        tmp = new int[n];
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        
        mergeSort(nums, 0, n - 1);
        
        for (int i = 0; i < n; i++) System.out.print(nums[i] + " ");
    }
}
```

