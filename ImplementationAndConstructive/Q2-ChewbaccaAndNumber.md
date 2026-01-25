## Problem A: Chewbacca and Number

### Problem Statement:

Luke Skywalker gave Chewbacca an integer number `x`. Chewbacca likes inverting digits in numbers. Inverting a digit `t` means replacing it with `9 - t`.

Help Chewbacca transform the initial number `x` into the **minimum possible positive number** by inverting some (possibly zero) digits.

**Constraints**:

* 1 ≤ x ≤ 10¹⁸
* The decimal representation of the final number should not start with a zero.

**Input:**
A single integer `x`.

**Output:**
Print the minimum possible positive number that Chewbacca can obtain after inverting some digits. The number should not have leading zeroes.

**Example 1:**
Input:

```
27
```

Output:

```
22
```

**Example 2:**
Input:

```
4545
```

Output:

```
4444
```

---

### Logic / Intuition:

1. For each digit `d` in the number, you have **two options**:

   * Keep the digit as it is.
   * Invert the digit: `9 - d`.
2. Always choose the **smaller of the two** to minimize the number.
3. **Special case for the first digit**:

   * It cannot be `0`.
   * If inverting the first digit results in `0`, keep the original digit.
4. Iterate through the number, apply the rule for each digit, and construct the new number.

**Example walkthrough:**
Number: `3184`

* 3 → invert to 6 → 6 > 3 → keep 3
* 1 → invert to 8 → 8 > 1 → keep 1
* 8 → invert to 1 → 1 < 8 → choose 1
* 4 → invert to 5 → 5 > 4 → keep 4

Final answer: `3114`

---

### C++ Solution:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string x;
    cin >> x;

    string ans = "";
    for(int i = 0; i < x.size(); i++) {
        int digit = x[i] - '0'; // Convert char to integer
        int inverted = 9 - digit;

        // For the first digit, don't allow leading zero
        if(i == 0 && inverted == 0) {
            ans += (digit + '0');
        } else {
            ans += (min(digit, inverted) + '0'); // Choose the smaller value
        }
    }

    cout << ans << "\n";
    return 0;
}
```

---

### Explanation of Key Parts:

1. `int digit = x[i] - '0';`

   * Converts a character `'0'`-`'9'` to its integer value.

2. `ans += (min(digit, inverted) + '0');`

   * Converts the integer back to a character and appends it to the answer string.

3. Special handling of the first digit to **avoid leading zeros**.

4. Final `cout << ans;` prints the transformed minimal number.

---

### Variations / Edge Cases:

* Input `9999` → Output `9000`
* Single-digit numbers → choose the smaller of the digit or its inversion.
* Large numbers up to 10¹⁸ can be handled as strings to avoid integer overflow.
