[791. 高精度加法](https://www.acwing.com/problem/content/793/)

#### 算法：

*#高精度加法*

#### 时间复杂度分析：

O(n)，n 为 A，B 中长度较长的数字的长度。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

vector<int> add(vector<int> &A, vector<int> &B) {
    // A 为长度较长的数，用于简化 for 中判断
    if (A.size() < B.size()) return add(B, A);
    
    vector<int> C;
    int t = 0; // 进位
    for (int i = 0; i < A.size(); i++) {
        t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }
    
    if (t) C.push_back(t);
    
    return C;
}

int main() {
    string a, b;
    cin >> a >> b;
    
    vector<int> A, B;
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
    
    auto C = add(A, B);
    for (int i = C.size() - 1; i >= 0; i--) cout << C[i];
    cout << endl;
    
    return 0;
}
```

