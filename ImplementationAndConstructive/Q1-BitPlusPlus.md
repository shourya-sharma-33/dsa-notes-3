## Codeforces Problem A: Bit++

### Problem Statement

Bitland’s programming language, **Bit++**, has exactly one variable `x`. There are only two operations:

* `++` increases `x` by 1
* `--` decreases `x` by 1

A statement consists of exactly **one operation** and the variable `x`. The operation can be **before or after** the variable.

A program is a sequence of statements executed in order. The initial value of `x` is 0.

**Input:**

* First line: integer `n` (1 ≤ n ≤ 150) — number of statements
* Next `n` lines: each line contains a statement (`++X`, `X++`, `--X`, `X--`)

**Output:**

* Final value of `x` after executing all statements

**Examples:**

Input:

```
1
++X
```

Output:

```
1
```

Input:

```
2
X++
--X
```

Output:

```
0
```

---

### Logic / Intuition

1. The program has **exactly one variable** (`x`) starting at 0.
2. For each statement:

   * If it contains `++` → increment `x`
   * If it contains `--` → decrement `x`
3. The **position of `++` or `--`** relative to `x` doesn’t matter.

This is essentially a **counting problem**:

* Count all increments and decrements and apply them to `x`.

---

### C++ Solution

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int n;
    cin >> n;

    int x = 0;
    for (int i = 0; i < n; i++) {
        string statement;
        cin >> statement;

        // Check if the statement contains "++"
        if (statement.find("++") != string::npos) {
            x++;
        } else {
            x--;
        }
    }

    cout << x << "\n";
    return 0;
}
```

---

### Explanation of Key Parts

1. `statement.find("++") != string::npos`

   * Checks if the string contains `++`
   * If true → increment `x`
   * Else → decrement `x`

2. No need to check order (`++X` or `X++`) because **both increment** the variable.

3. Iterating over all `n` statements ensures every operation is applied sequentially.

---

### Edge Cases

* All increments → `x = n`
* All decrements → `x = -n`
* Mixed statements → `x` is difference between counts of `++` and `--`

---

This is a **classic beginner-level implementation problem** focused on string checking and simple loops.

