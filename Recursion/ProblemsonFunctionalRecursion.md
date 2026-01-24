# Reverse Array & Palindrome Check (Recursion)

---

## 1. Reverse an Array (Two Pointers)

### Problem
Reverse:
```

[a, b, c, d] → [d, c, b, a]

````

### Idea
- Use two pointers:
  - `l` → start
  - `r` → end
- Swap
- Move inward (`l+1`, `r-1`)

---

### Recursive Function (Two Pointers)

```cpp
void reverse(int l, int r, vector<int>& arr) {
    if (l >= r) return;

    swap(arr[l], arr[r]);
    reverse(l + 1, r - 1, arr);
}
````

### Call

```cpp
reverse(0, n - 1, arr);
```

---

## 2. More Efficient Reverse (Single Index)

### Observation

* Only need to go till **middle**
* Second index can be derived

### Base Condition

```
i >= n / 2
```

---

### Recursive Function (Optimized)

```cpp
void reverse(int i, vector<int>& arr, int n) {
    if (i >= n / 2) return;

    swap(arr[i], arr[n - i - 1]);
    reverse(i + 1, arr, n);
}
```

### Call

```cpp
reverse(0, arr, n);
```

---

## 3. Check Palindrome (String)

### Problem

```
"madam" → palindrome
"abc"   → not palindrome
```

---

### Idea

* Compare symmetric characters
* Stop at middle
* If mismatch → false

---

### Recursive Palindrome Check

```cpp
bool isPalindrome(int i, string& s, int n) {
    if (i >= n / 2) return true;

    if (s[i] != s[n - i - 1]) return false;

    return isPalindrome(i + 1, s, n);
}
```

### Call

```cpp
bool ans = isPalindrome(0, s, s.size());
```

---

## 4. Key Patterns

### Reverse Array

* Swap symmetric elements
* Shrink problem size
* Stop at middle

### Palindrome

* Compare symmetric characters
* Early termination on mismatch

---

## 5. Summary Table

| Problem       | Technique         | Base Condition |
| ------------- | ----------------- | -------------- |
| Reverse Array | Swap + recurse    | `i >= n/2`     |
| Palindrome    | Compare + recurse | `i >= n/2`     |
| Two Pointer   | `l++, r--`        | `l >= r`       |

---

## Key Takeaways

* Always move **towards the center**
* `n - i - 1` gives symmetric index
* Recursion reduces problem size every call
* Same template works for many problems

---


