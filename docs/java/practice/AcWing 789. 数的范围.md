[789. 数的范围](https://www.acwing.com/problem/content/791/)

#### 算法：

*#二分搜索*

#### 时间复杂度分析：

每次判断都会将数据规模减少一半，所以最多判断 logn 次，时间复杂度为 O(logn)。

#### 代码：

```java
import java.util.*;

class Main {
    static int n, q;
    static int[] nums;
    
    static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        q = sc.nextInt();
        nums = new int[n];
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        
        while (q-- > 0) {
            int l = 0, r = n - 1, x = sc.nextInt();
            while (l < r) {
                int mid = l + r >> 1;
                if (nums[mid] >= x) r = mid;
                else l = mid + 1;
            }
            
            if (nums[l] != x) System.out.println("-1 -1");
            else {
                System.out.print(l + " ");
                l = 0;
                r = n - 1;
                while (l < r) {
                    int mid = l + r + 1 >> 1;
                    if (nums[mid] <= x) l = mid;
                    else r = mid - 1;
                }
                
                System.out.println(r);
            }
        }
    }
}
```

