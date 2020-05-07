[803. 区间合并](https://www.acwing.com/problem/content/805/)

#### 算法：

*#区间合并*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef pair<int, int> PII;

void merge(vector<PII> &segs) {
    sort(segs.begin(), segs.end());
    
    vector<PII> ret;
    int st = -2e9, ed = -2e9;
    for (auto seg : segs) {
        if (seg.first > ed) {
            if (st != -2e9) ret.push_back({st, ed});
            st = seg.first, ed = seg.second;
        } else {
            ed = max(ed, seg.second);
        }
    }
    
    if (st != -2e9) ret.push_back({st, ed});
    
    segs = ret;
}

int main() {
    int n;
    cin >> n;
    
    vector<PII> segs;
    while (n--) {
        int l, r;
        scanf("%d%d", &l, &r);
        segs.push_back({l, r});
    }
    
    merge(segs);
    cout << segs.size() << endl;
    
    return 0;
}
```

