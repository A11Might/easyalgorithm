[803. 区间合并](https://www.acwing.com/problem/content/805/)

#### 算法：

*#区间合并*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

public class Main {
    private static int merge(List<int[]> segs) {
        List<int[]> ret = new ArrayList<>();
        
        int st = (int) -2e9, ed = (int) -2e9;
        for (var seg : segs) {
            if (ed < seg[0]) {
                if (ed != -2e9) ret.add(new int[] {st, ed});
                st = seg[0];
                ed = seg[1];
            } else {
                ed = Math.max(ed, seg[1]);
            }
        }
        if (ed != -2e9) ret.add(new int[] {st, ed});
        
        return ret.size();
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        List<int[]> segs = new ArrayList<>();
        while (n-- > 0) {
            int l = sc.nextInt(), r = sc.nextInt();
            segs.add(new int[] {l, r});
        }
        
        segs.sort((o1, o2) -> o1[0] - o2[0]);
        System.out.println(merge(segs));
    }
}
```

