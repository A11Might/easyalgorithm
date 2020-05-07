[786. 第k个数](https://www.acwing.com/problem/content/788/)

#### 算法：

*#快速排序*

**快速选择算法：**

1. 找到分界点x：可以是 nums[l]、nums[r] 或者 nums[(l + r) / 2]。
2. 划分区间：将数组划分为 left：元素都 <= x，元素个数为 S<sub>L</sub> 的左半部分和 right：元素都 >= x，元素个数为 S<sub>R</sub> 右半部分。
   - k <= S<sub>L</sub>，第 k 个数在左半边，递归 left 部分查找。
   - k > S<sub>L</sub>，第 k 个数在右半边，递归 right 部分查找，去求右半边的第 k - S<sub>L</sub> 个元素。

递归中我们一直保证数组第 k 小元素在区间[l, r]内，这样当区间长度为 1 时，区间中的元素就是答案。

#### 时间复杂度分析：

根据递归树分析：

递归树第一层需要遍历整个数组，第二层减半，第三层再减半，以此类推，时间复杂度是 n + (1 / 2) * n + (1 / 4) * n + ... + 1 = O(n)。

#### 代码：

```java
import java.util.*;

class Main {
    static int n, k;
    static int[] nums;
    
    static int quickSort(int[] nums, int l, int r, int k) {
        if (l >= r) return nums[l];
        
        int i = l - 1, j = r + 1, x = nums[l + r >> 1];
        while (i < j) {
            do i++; while (nums[i] < x);
            do j--; while (nums[j] > x);
            if (i < j) {
                int tmp = nums[j];
                nums[j] = nums[i];
                nums[i] = tmp;
            }
        }
        
        int sl = j - l + 1;
        if (k <= sl) return quickSort(nums, l, j, k);
        return quickSort(nums, j + 1, r, k - sl);
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        k = sc.nextInt();
        nums = new int[n];
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        
        System.out.println(quickSort(nums, 0, n - 1, k));
    }
}
```

