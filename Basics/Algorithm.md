

# STL Algorithms (C++ Notes)

## 1. `sort()` — Basic Sorting

### 1.1 Sorting an Array

```cpp
int a[] = {1, 5, 3, 2};
sort(a, a + 4);
```

* `a` → starting iterator (included)
* `a + 4` → ending iterator (excluded)
* Sorts entire array in **ascending order**
* Result: `1 2 3 5`

> STL uses **[start, end)** convention

---

### 1.2 Sorting a Vector

```cpp
vector<int> v = {1, 5, 3, 2};
sort(v.begin(), v.end());
```

* Works for all **sequence containers**
* (`array`, `vector`, `deque`)
* ❌ Not for `map`, `set`

---

### 1.3 Sorting a Subarray / Subvector

```cpp
int a[] = {5, 2, 1, 3};
sort(a + 2, a + 4);
```

* Sorts only index `[2, 3]`
* Partial range sorting supported

---

### 1.4 Sorting in Descending Order

```cpp
sort(a, a + n, greater<int>());
```

* `greater<int>()` → built-in comparator
* Sorts in **descending order**

---

## 2. Custom Comparator (`my way` sorting)

### 2.1 When Comparator is Needed

* Sorting in **non-standard logic**
* Example:

  * Sort by **second element (ascending)**
  * If equal, sort by **first element (descending)**

---

### 2.2 Comparator Rules

* Comparator returns **bool**
* Takes **two elements (p1, p2)**
* Returns `true` if `p1` should come **before** `p2`

---

### 2.3 Example: Pair Sorting

```cpp
bool cmp(pair<int,int> p1, pair<int,int> p2) {
    if (p1.second < p2.second) return true;
    if (p1.second > p2.second) return false;
    return p1.first > p2.first;
}
```

Usage:

```cpp
sort(v.begin(), v.end(), cmp);
```

---

### 2.4 Comparator Thinking Model

* **Never think about array**
* Always think:

  * Compare **two elements**
  * Decide: **correct order or not**
* If comparator returns `false` → STL swaps internally

---

## 3. `__builtin_popcount`

### 3.1 Count Set Bits (int)

```cpp
int x = 7;          // 111
int bits = __builtin_popcount(x); // 3
```

* Returns number of `1` bits
* Works on 32-bit integers

---

### 3.2 For `long long`

```cpp
long long x = 6;
int bits = __builtin_popcountll(x);
```

---

## 4. `next_permutation`

### 4.1 What It Does

* Generates **next lexicographical permutation**
* Returns:

  * `true` → next permutation exists
  * `false` → no more permutations

---

### 4.2 Printing All Permutations

```cpp
string s = "123";
sort(s.begin(), s.end());

do {
    cout << s << endl;
} while (next_permutation(s.begin(), s.end()));
```

* Must **start from sorted order**
* Total permutations = `n!`

---

### 4.3 Important Catch

If you start from `"231"`:

* Output will be:

  * `231`
  * `312`
  * `321`
* ❌ Not all permutations

✅ Always `sort()` first

---

## 5. `max_element` / `min_element`

### 5.1 Maximum Element

```cpp
int a[] = {1, 5, 6};
int mx = *max_element(a, a + 3);
```

* Returns **iterator**
* Use `*` to get value

---

### 5.2 Minimum Element

```cpp
int mn = *min_element(a, a + 3);
```

---

## 6. Summary (CP-Relevant STL)

| Algorithm            | Use                   |
| -------------------- | --------------------- |
| `sort()`             | Fast sorting          |
| Custom Comparator    | Custom order          |
| `greater<>`          | Descending sort       |
| `__builtin_popcount` | Count set bits        |
| `next_permutation`   | Generate permutations |
| `max_element`        | Find max              |
| `min_element`        | Find min              |
