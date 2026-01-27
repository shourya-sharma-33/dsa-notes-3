# Codeforces Round 287 (Div. 2)

## Problem A: Amr and Music

### Problem Statement

Amr has `n` musical instruments. Learning the `i`th instrument takes `a[i]` days.

Amr has exactly `k` days and wants to learn the **maximum number of instruments** possible.

You need to output

1. The maximum number of instruments Amr can learn
2. The indices of those instruments

If there are multiple valid answers, print any.

---

### Input

First line: two integers `n` and `k`
Second line: `n` integers where `a[i]` is the number of days required for the `i`th instrument

---

### Output

First line: integer `m`, the maximum number of instruments
Second line: `m` space separated indices of instruments

---

### Key Observation

To learn the **maximum number of instruments**, Amr should always learn the instruments that take **minimum days first**.

This is a classic **greedy strategy**.

---

### Logic / Intuition

1. Each instrument has:
   days required
   original index

2. Sort the instruments based on **days required**.

3. Start picking instruments from the smallest days:
   if remaining days `k` is enough
   subtract the days
   count the instrument

4. Stop when you cannot afford the next instrument.

This guarantees the maximum count because choosing cheaper instruments first always allows more selections.

---

### Case Analysis

Input:

```
5 6
4 3 1 1 2
```

Indexed view:

```
Index     : 1  2  3  4  5
Days      : 4  3  1  1  2
```

All possible valid combinations:

```
(1 = 4, 5 = 2)
(1 = 4, 3 = 1, 4 = 1)
(2 = 3, 3 = 1, 4 = 1)
(3 = 1, 4 = 1, 5 = 2)
(2 = 3, 5 = 2)
```

The best choice gives **3 instruments**, which is the maximum.

---

### Greedy Strategy Used

Sort instruments by days:

```
(1 day: index 3)
(1 day: index 4)
(2 days: index 5)
(3 days: index 2)
(4 days: index 1)
```

Pick in this order until `k` runs out.

---

### C++ Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;

    vector<pair<int, int>> v;

    for (int i = 0; i < n; i++) {
        int days;
        cin >> days;
        v.push_back({days, i + 1});
    }

    sort(v.begin(), v.end());

    vector<int> indices;

    for (int i = 0; i < n; i++) {
        if (v[i].first <= k) {
            k -= v[i].first;
            indices.push_back(v[i].second);
        } else {
            break;
        }
    }

    cout << indices.size() << "\n";
    for (int idx : indices) {
        cout << idx << " ";
    }
    cout << "\n";

    return 0;
}
```

---

### Explanation of Key Parts

1. `vector<pair<int,int>> v`
   Stores `(days_required, instrument_index)`

2. `sort(v.begin(), v.end())`
   Automatically sorts by days required

3. Greedy loop
   Always picks the cheapest remaining instrument

4. `indices.size()`
   Gives the maximum number of instruments learned

---

### Time and Space Complexity

Time Complexity: O(n log n) due to sorting
Space Complexity: O(n)

---

### Edge Cases

* `k = 0` → answer is 0
* Only one instrument and insufficient days → answer is 0
* Enough days to learn all instruments → take all

