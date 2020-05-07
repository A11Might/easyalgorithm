[803. 区间合并](https://www.acwing.com/problem/content/805/)

#### 算法：

*#区间合并*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static List<int[]> merge(List<int[]> segs) {
        List<int[]> ret = new ArrayList<>();

        int st = Integer.MIN_VALUE, ed = Integer.MIN_VALUE;
        for (int[] seg : segs) {
            if (seg[0] > ed) {
                if (ed != Integer.MIN_VALUE) ret.add(new int[] {st, ed});
                st = seg[0];
                ed = seg[1];
            } else {
                ed = Math.max(ed, seg[1]);
            }
        }

        if (ed != Integer.MIN_VALUE) ret.add(new int[] {st, ed});

        return ret;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        List<int[]> segs = segs = new ArrayList<>(n);
        for (int i = 0; i < n; i++) {
            int l = sc.nextInt(), r = sc.nextInt();
            segs.add(new int[] {l, r});
        }

        segs.sort((o1, o2) -> o1[0] - o2[0]);
        var ret = merge(segs);

        System.out.println(ret.size());
    }
}
```

