[803. 区间合并](https://www.acwing.com/problem/content/805/)

#### 算法：

*#区间合并*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

#define PII pair<int, int>
#define x first
#define y second

using namespace std;

int n;
vector<PII> seqs;

void merge(vector<PII> &seqs) {
    sort(seqs.begin(), seqs.end());
    
    vector<PII> ret;
    int st = -2e9, ed = -2e9;
    for (auto seq : seqs) {
        if (seq.x > ed) {
            if (st != -1e9) ret.push_back({st, ed});
            st = seq.x, ed = seq.y;
        } else {
            ed = max(ed, seq.y);
        }
    }
    
    seqs = ret;
}

int main() {
    scanf("%d", &n);
    while (n--) {
        int l, r;
        scanf("%d%d", &l, &r);
        seqs.push_back({l, r});
    }
    
    merge(seqs);
    cout << seqs.size() << endl;
    
    return 0;
}
```

