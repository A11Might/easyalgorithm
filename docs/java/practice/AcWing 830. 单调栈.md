[830. 单调栈](https://www.acwing.com/problem/content/832/)

#### 算法：

*#单调栈*

同双指针算法一样，先想一下朴素算法，再挖掘一些性质，将目光集中在较少的状态上，从而将时间复杂度降低。

**朴素算法 O(n<sup>2</sup>)**

使用 i 指针遍历数组，每次遍历固定 i 指针，向前枚举元素 j，直到找到第一个比 i 指针指向元素小的元素。

```java
for (int i = 0; i < n; i++) {
    for (int j = i - 1; j >= 0; j--) {
        if (a[i] > a[j]) {
            System.out.println(a[j]);
            break;
        }
    }
}
```

在遍历 i 的过程中，我们可以使用栈存储当前元素 ai 前面的元素。通过观察发现，当元素 ax >= ay 并且 x < y 时，ax 永远不会作为答案输出。因为当 ax < ai 时，ay 也小于 ai（ax >= ay），但 ay 离 ai 更近，所以会返回 ay。

所以如果当前元素 ai 前面的元素存在逆序的情况，我们就可以删除逆序对中较大的元素。当删除所有逆序后，栈中剩余的元素就是单调递增的了。

**具体算法**

1. 当前元素 i >= stk[tt]，由于元素 i 会压入栈中，stk[tt] 永远不会作为答案输出，所以我们弹出栈顶。
2. 当前元素 i < stk[tt]，找到离元素 i 最近的比它小的元素，输出后将元素 i 压入栈中。

#### 时间复杂度分析：

每个元素只会进栈和出栈一次，所以时间复杂度为 O(n)。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int tt = 0;
    static int[] stk = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while (n-- > 0) {
            int x = sc.nextInt();
            while (tt != 0 && stk[tt] >= x) tt--;
            if (tt == 0) System.out.print(-1 + " ");
            else System.out.print(stk[tt] + " ");
            stk[++tt] = x;
        }
    }
}
```

