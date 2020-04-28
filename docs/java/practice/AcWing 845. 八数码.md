[845. 八数码](https://www.acwing.com/problem/content/847/)

#### 算法：

*#bfs*

将棋盘的状态抽象成节点，如果状态 a 能转化成状态 b的话，就连一条 a 到 b 的边，这样就将题目抽象成了图，问题就变成了寻找从起到到终点最短的距离，所有边的权重都是 1，所以可以使用宽搜。

需要考虑的点：

- 如何把状态存入队列：将每个状态的棋盘展成一行，用一个字符串表示。

- 如何记录每个状态的距离：使用 HashMap<String, Integer> 存储。
- 状态之间怎么转化：将表示一个状态的字符串恢复成棋盘，进行数字交换后，再用字符串表示成另一个状态。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static int[][] dir = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    static int bfs(String state) {
        Queue<String> q = new ArrayDeque<>();
        HashMap<String, Integer> d = new HashMap<>();

        q.offer(state);
        d.put(state, 0);

        String end = "12345678x";
        while (!q.isEmpty()) {
            String u = q.poll();
            if (u.equals(end)) return d.get(u);

            int distance = d.get(u);
            int k = u.indexOf('x');
            int i = k / 3, j = k % 3;
            for (var dd : dir) {
                int x = i + dd[0], y = j + dd[1];
                if (x < 0 || x >= 3 || y < 0 || y >= 3) continue;
                u = swap(u, x * 3 + y, k);
                if (!d.containsKey(u)) {
                    d.put(u, distance + 1);
                    q.offer(u);
                }
                u = swap(u, x * 3 + y, k);
            }
        }

        return -1;
    }

    static String swap(String str, int a, int b) {
        char[] ret = str.toCharArray();
        char tmp = ret[b];
        ret[b] = ret[a];
        ret[a] = tmp;
        return new String(ret);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String start = sc.nextLine().replaceAll(" ", "");

        System.out.println(bfs(start));
    }
}
```

