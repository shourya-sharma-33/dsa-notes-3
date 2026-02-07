# Codeforces Round 548 (Div. 2)
## Problem B: Chocolates

### Problem Statement

There are `n` types of chocolates. For each type `i`, there are `a[i]` chocolates available in the store.

You want to buy chocolates such that if you buy `x[i]` chocolates of type `i`, then for **every** `j < i`, **at least one** of the following must be true:

x[j] = 0
x[j] < x[i]

Your goal is to **maximize the total number of chocolates bought**.

**Input:**

* An integer `n` denoting number of chocolate types
* An array `a` of size `n` where `a[i]` is the stock of chocolate type `i`

**Output:**

* Print the maximum number of chocolates you can buy

---

### Key Observation

The condition means that when moving from **left to right**, the number of chocolates bought must be **strictly increasing**, ignoring zeros.

Instead of thinking forward, it is easier to think **backwards**:

If you decide how many chocolates to buy from type `i`, then type `i-1` must have **strictly fewer** chocolates than that.

So the decision for `i-1` depends on `i`.

---

### Logic / Intuition

1. Start from the **last chocolate type**, since it has no restriction.
2. Buy as many chocolates as possible from the last type.
3. Move backwards:

   * For each type `i`, you can buy **at most**:

     * `a[i]`
     * `previous_value - 1`
   * This ensures the strictly increasing condition.
4. If the allowed maximum becomes `0`, stop because earlier types must be `0`.

This greedy approach works because taking the maximum possible at each step always leads to the maximum total sum.

---

### Example Walkthrough

Input:

```
1 2 1 3 6
```

Start from the back:

* Type 5: take 6
* Type 4: max allowed is 5, stock is 3 → take 3
* Type 3: max allowed is 2, stock is 1 → take 1
* Type 2: max allowed is 0 → stop

Final selection:

```
0 0 1 3 6
```

Sum = 10

---

### C++ Solution

```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;

    long long arr[n];
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    long long ans = 0;

    // Start from the last element
    ans += arr[n - 1];
    long long mx = arr[n - 1] - 1;

    // Traverse backwards
    for (int i = n - 2; i >= 0; i--) {
        if (mx <= 0) break;

        long long take = min(mx, arr[i]);
        ans += take;
        mx = take - 1;
    }

    cout << ans << "\n";
    return 0;
}
```

---

### Explanation of Key Parts

1. `mx`

   * Represents the **maximum chocolates allowed** for the current type
   * Ensures strict inequality with the next type

2. `take = min(mx, arr[i])`

   * You cannot exceed stock
   * You cannot violate the increasing condition

3. `mx = take - 1`

   * Ensures the next left type is strictly smaller

4. Early stopping when `mx == 0`

   * All earlier types must be zero

---

### Time and Space Complexity

* Time Complexity: O(n)
* Space Complexity: O(1) additional space

---

### Edge Cases

* All values equal → answer is 1
* Strictly increasing array → take all chocolates
* Large values handled using `long long`

