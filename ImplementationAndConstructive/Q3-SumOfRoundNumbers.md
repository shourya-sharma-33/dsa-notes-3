## Problem A: Sum of Round Numbers

### Problem Statement

A positive integer is called **round** if it is of the form `d00...0`. In other words, a number is round if all its digits except the **most significant** are zeros. Numbers from 1 to 9 are also considered round.

Given a positive integer `n`, represent it as a **sum of the minimum number of round numbers**.

**Input:**

* First line: integer `t` (1 ≤ t ≤ 10⁴) — number of test cases
* Next `t` lines: each line contains an integer `n` (1 ≤ n ≤ 10⁴)

**Output:**
For each test case, output:

1. An integer `k` — the minimum number of round numbers
2. `k` round numbers whose sum is `n`

**Example:**

Input:

```
5
5009
7
9876
10000
10
```

Output:

```
2
5000 9
1
7
4
8000 70 6 900
1
10000
1
10
```

---

### Logic / Intuition

1. A **round number** has the form `d * 10^k`. For each digit in `n`, if it is non-zero, it contributes a round number of the same value.
2. **Strategy**:

   * Process the number **digit by digit from least significant**
   * Multiply each non-zero digit by its positional value to get a round number
   * Store these round numbers in a vector
3. The **number of summands** is equal to the number of non-zero digits.

**Example walkthrough:**
Number: `5009`

* Split digits by place value:

  * 9 → 9 (round number)
  * 0 → skip
  * 0 → skip
  * 5 → 5000 (round number)

Answer: `5000 + 9`

---

### C++ Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve() {
    int n;
    cin >> n;

    vector<int> rounds;
    int place = 1; // Start with units place

    while (n > 0) {
        int digit = n % 10; // Get the last digit
        if (digit != 0) {
            rounds.push_back(digit * place); // Multiply by place value to form round number
        }
        n /= 10; // Remove the last digit
        place *= 10; // Move to next place value (tens, hundreds, ...)
    }

    cout << rounds.size() << "\n"; // Number of summands
    for (int i = 0; i < rounds.size(); i++) {
        cout << rounds[i] << " ";
    }
    cout << "\n";
}

int main() {
    int t;
    cin >> t;
    while (t--) {
        solve();
    }
    return 0;
}
```

---

### Explanation of Key Parts

1. `int digit = n % 10;`

   * Extracts the last digit of the number

2. `rounds.push_back(digit * place);`

   * Converts a single digit into a round number based on its position (units, tens, hundreds...)

3. `n /= 10; place *= 10;`

   * Move to the next higher place value for the next digit

4. `rounds.size()` gives the **minimum number of summands**, which is the count of non-zero digits.

---

### Edge Cases

* Single-digit numbers → already round, only 1 summand
* Numbers with zeros in between digits → skip zeros
* Maximum input `n = 10⁴` → can be handled easily with this digit-wise approach

---

This approach is simple, **O(number of digits)** per test case, and avoids unnecessary pre-stored arrays.

