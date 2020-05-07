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
    static int n;
    static int[] nums;
    
    static void quickSort(int[] nums, int l, int r) {
        if (l == r) return;
        
        int i = l - 1, j = r + 1, x = nums[(l + r) >> 1];
        while (i < j) {
            do i++; while (nums[i] < x);
            do j--; while (nums[j] > x);
            if (i < j) {
                int tmp = nums[j];
                nums[j] = nums[i];
                nums[i] = tmp;
            }
        }
        
        quickSort(nums, l, j);
        quickSort(nums, j + 1, r);
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        nums = new int[n];
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        quickSort(nums, 0, n - 1);
        
        for (int i = 0; i < n; i++) System.out.print(nums[i] + " ");
    }
}
```

