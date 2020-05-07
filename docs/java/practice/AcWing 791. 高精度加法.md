[791. 高精度加法](https://www.acwing.com/problem/content/793/)

#### 算法：

*#高精度加法*

#### 时间复杂度分析：

O(n)，n 为 A，B 中长度较长的数字的长度。

#### 代码：

```java
import java.util.*;

class Main {
    static List<Integer> add(List<Integer> A, List<Integer> B) {
        if (B.size() > A.size()) return add(B, A); // A 为长度较长的数，用于简化 for 中判断
        
        List<Integer> C = new ArrayList<>();
        int t = 0; // 进位
        for (int i = 0; i < A.size(); i++) {
            t += A.get(i);
            if (i < B.size()) t += B.get(i);
            C.add(t % 10);
            t /= 10;
        }
        
        if (t != 0) C.add(t);
        return C;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.nextLine(), b = sc.nextLine();
        List<Integer> A = new ArrayList<>();
        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        List<Integer> B = new ArrayList<>();
        for (int i = b.length() - 1; i >= 0; i--) B.add(b.charAt(i) - '0');
        
        List<Integer> C = add(A, B);
        
        for (int i = C.size() - 1; i >= 0; i--) System.out.print(C.get(i));
    }
}
```

