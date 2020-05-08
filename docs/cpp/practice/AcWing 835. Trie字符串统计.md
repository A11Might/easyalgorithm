[835. Trie字符串统计](https://www.acwing.com/problem/content/837/)

#### 算法：

*#Trie树*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int son[N][26], cnt[N], idx;
char str[N];

void insert(char str[]) {
    int p = 0; // 从根结点开始，0 号点既是根节点，又是空节点
    for (int i = 0; str[i]; i++) {
        int u = str[i] - 'a';
        if (!son[p][u]) son[p][u] = ++idx;
        p = son[p][u];      
    }
    cnt[p]++;
}

int query(char str[]) {
    int p = 0; // 从根结点开始，0 号点既是根节点，又是空节点
    for (int i = 0; str[i]; i++) {
        int u = str[i] - 'a';
        if (!son[p][u]) return 0;
        p = son[p][u];
    }
    return cnt[p];
}

int main() {
    int n;
    cin >> n;
    while (n--) {
        char op;
        cin >> op >> str;
        if (op == 'I') insert(str);
        else cout << query(str) << endl;;
    }
    
    return 0;
}
```

