[845. 八数码](https://www.acwing.com/problem/content/847/)

#### 算法：

*#bfs*

将棋盘的状态抽象成节点，如果状态 a 能转化成状态 b的话，就连一条 a 到 b 的边，这样就将题目抽象成了图，问题就变成了寻找从起到到终点最短的距离，所有边的权重都是 1，所以可以使用宽搜。

需要考虑的点：

- 如何把状态存入队列：将每个状态的棋盘展成一行，用一个字符串表示。

- 如何记录每个状态的距离：使用 unordered_map<string, int> 存储。
- 状态之间怎么转化：将表示一个状态的字符串恢复成棋盘，进行数字交换后，再用字符串表示成另一个状态。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <algorithm>
#include <queue>
#include <unordered_map>

using namespace std;

int dx[] = {-1, 0, 1, 0}, dy[] = {0, 1, 0, -1};
string last = "12345678x";

int main() {
    string start;
    char c;
    while (cin >> c) start += c;
    
    queue<string> q;
    unordered_map<string, int> d;
    
    q.push(start);
    d[start] = 0;
    
    while (q.size()) {
        auto u = q.front();
        q.pop();
        
        if (u == last) {
            cout << d[u] << endl;
            return 0;
        }
        
        int distance = d[u];
        int k = u.find('x');
        int x = k / 3, y = k % 3;
        for (int i = 0; i < 4; i++) {
            int a = x + dx[i], b = y + dy[i];
            if (a < 0 || a >= 3 || b < 0 || b >= 3) continue;
            swap(u[a * 3 + b], u[k]);
            if (!d.count(u)) {
                d[u] = distance + 1;
                q.push(u);
            }
            swap(u[a * 3 + b], u[k]);
        }
    }
    
    cout << -1 << endl;
    return 0;
}
```

