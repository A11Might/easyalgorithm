[791. 高精度加法](https://www.acwing.com/problem/content/793/)

#### 算法：

*#高精度加法*

#### 时间复杂度分析：

O(n)，n 为 A，B 中长度较长的数字的长度。

#### 代码：

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next(), b = sc.next();
        List<Integer> A = new ArrayList<>(), B = new ArrayList<>();
        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        for (int i = b.length() - 1; i >= 0; i--) B.add(b.charAt(i) - '0');
        
        var C = add(A, B);
        for (int i = C.size() - 1; i >= 0; i--) System.out.print(C.get(i));
    }
    
    static List<Integer> add(List<Integer> A, List<Integer> B) {
        List<Integer> C = new ArrayList<>();
        
        int t = 0; // 进位
        for (int i = 0; i < A.size() || i < B.size() || t != 0; i++) {
            if (i < A.size()) t += A.get(i);
            if (i < B.size()) t += B.get(i);
            C.add(t % 10);
            t /= 10;
        }
        
        return C;
    }
}
```

