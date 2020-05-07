[792. 高精度减法](https://www.acwing.com/problem/content/description/794/)

#### 算法：

*#高精度减法*

#### 时间复杂度分析：

O(n)，n 为 A，B 中长度较长的数字的长度。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

// 判断 A 是否大于等于 B
bool cmp(vector<int> &A, vector<int> &B) {
    if (A.size() != B.size()) return A.size() > B.size();
    
    for (int i = A.size() - 1; i >= 0; i--) {
        if (A[i] != B[i]) return A[i] > B[i];
    }
    return true;
}

vector<int> sub(vector<int> &A, vector<int> &B) {
    vector<int> C;
    int t = 0; // 借位
    for (int i = 0; i < A.size(); i++) {
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }
    
    // 去除先导 0
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    
    return C;
}

int main() {
    string a, b;
    cin >> a >> b;
    
    vector<int> A, B;
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i--) B.push_back(b[i] - '0');
    
    vector<int> C;
    if (cmp(A, B)) C = sub(A, B);
    else C = sub(B, A), cout << '-';
    
    for (int i = C.size() - 1; i >= 0; i--) cout << C[i];
    cout << endl;
    
    return 0;
}
```

