# Educational Codeforces Round 49 Div. 2

## Problem A: Palindromic Twist

### Problem Statement

You are given a string `s` of even length `n`.

For every position in the string, you must change the character **exactly once**:

* Either to the **previous** letter in the alphabet
* Or to the **next** letter in the alphabet

Special cases:

* `'a'` can only change to `'b'`
* `'z'` can only change to `'y'`

After applying these changes to **all characters**, check whether the resulting string **can be a palindrome**.

---

### Definition

A string is a palindrome if it is the same when read from left to right and right to left.

Examples:

* `abba` is a palindrome
* `abca` is not

---

### Key Observation

For the final string to be a palindrome:

* Characters at symmetric positions `i` and `n - i - 1` must become **equal**

Each character can only move **one step** forward or backward in the alphabet.

So for a pair `(s[i], s[j])`, we must check:

* Whether both characters can be shifted so that they become the same letter

---

### Core Logic / Intuition

For every symmetric pair `(s[i], s[j])`:

* Each character can change by exactly **1 alphabet step**
* After the change, the two characters must match

This is possible **if and only if**:

```
abs(s[i] - s[j]) == 0 OR abs(s[i] - s[j]) == 2
```

Why:

* Difference `0`: both characters are same, shift one up and the other down
* Difference `2`: both can move one step toward the middle character
* Difference `1` or greater than `2`: impossible to make them equal in one move

---

### Example Analysis

String: `adfa`

Pairs:

* `a` and `a`: difference 0 → valid
* `d` and `f`: difference 2 → valid

Result: YES

---

String: `cf`

Pairs:

* `c` and `f`: difference 3 → invalid

Result: NO

---

### Algorithm

1. Initialize two pointers:

   * `i = 0`
   * `j = n - 1`
2. While `i < j`:

   * Compute `diff = abs(s[i] - s[j])`
   * If `diff` is not `0` and not `2`, print NO and return
3. If all pairs are valid, print YES

---

### Correct C++ Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve() {
    int n;
    cin >> n;

    string s;
    cin >> s;

    int i = 0, j = n - 1;

    while (i < j) {
        int diff = abs(s[i] - s[j]);
        if (diff != 0 && diff != 2) {
            cout << "NO\n";
            return;
        }
        i++;
        j--;
    }

    cout << "YES\n";
}

int main() {
    int T;
    cin >> T;

    while (T--) {
        solve();
    }

    return 0;
}
```

---

### Explanation of Important Parts

1. `abs(s[i] - s[j])`
   Converts character difference into numeric distance in alphabet

2. Condition `diff != 0 && diff != 2`
   Filters out impossible transformations

3. Two pointer approach
   Ensures palindrome symmetry is respected

---

### Time and Space Complexity

* Time Complexity: O(n) per string
* Space Complexity: O(1)

---

### Edge Cases

* All characters same
* Characters at alphabet boundaries like `a` and `z`
* Minimal length string `n = 2`

