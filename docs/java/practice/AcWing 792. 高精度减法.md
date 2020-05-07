[792. 高精度减法](https://www.acwing.com/problem/content/description/794/)

#### 算法：

*#高精度减法*

#### 时间复杂度分析：

O(n)，n 为 A，B 中长度较长的数字的长度。

#### 代码：

```java
import java.util.*;

class Main {
    // 判断 A 是否大于等于 B
    static boolean cmp(List<Integer> A, List<Integer> B) {
        if (A.size() != B.size()) return A.size() > B.size();
        
        for (int i = A.size() - 1; i >= 0; i--) {
            if (A.get(i) != B.get(i)) return A.get(i) > B.get(i);
        }
        return true;
    }
    
    static List<Integer> sub(List<Integer> A, List<Integer> B) {
        List<Integer> C = new ArrayList<>();
        
        int t = 0; // 借位
        for (int i = 0; i < A.size(); i++) {
             t = A.get(i) - t;
             if (i < B.size()) t -= B.get(i);
             C.add((t + 10) % 10);
             if (t >= 0) t = 0;
             else t = 1;
        }
        
        // 去除前导 0
        while (C.size() > 1 && C.get(C.size() - 1) == 0) C.remove(0);
        return C;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.nextLine(), b = sc.nextLine();
        List<Integer> A = new ArrayList<>();
        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        List<Integer> B = new ArrayList<>();
        for (int i = b.length() - 1; i >= 0; i--) B.add(b.charAt(i) - '0');
        
        List<Integer> C = new ArrayList<>();
        if (cmp(A, B)) C = sub(A, B);
        else {
            C = sub(B, A);
            System.out.print("-");
        }
        
        for (int i = C.size() - 1; i >= 0; i--) System.out.print(C.get(i));
    }
}
```

