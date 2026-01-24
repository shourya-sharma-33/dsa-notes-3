# Recursion Practice Problems (Basic)

---

## 1. Print a Name **N times**

### Idea
- Use a counter `i`
- Print first, then recurse
- Stop when `i > n`

```cpp
void f(int i, int n) {
    if (i > n) return;

    cout << "recursion" << endl;
    f(i + 1, n);
}
````

**Call**

```cpp
f(1, n);
```

---

## 2. Print Numbers from **1 to N**

### Idea

* Print before recursive call
* Increasing order

```cpp
void f(int i, int n) {
    if (i > n) return;

    cout << i << " ";
    f(i + 1, n);
}
```

**Call**

```cpp
f(1, n);
```

---

## 3. Print Numbers from **N to 1** (Using Extra Parameter)

### Idea

* Use `i` as counter
* Calculate value using `n - i + 1`

```cpp
void f(int i, int n) {
    if (i > n) return;

    cout << (n - i + 1) << " ";
    f(i + 1, n);
}
```

**Call**

```cpp
f(1, n);
```

---

## 4. Print Numbers from **N to 1** (Direct `i--`)

### Idea

* Start from `n`
* Decrease `i`
* Stop when `i < 1`

```cpp
void f(int i) {
    if (i < 1) return;

    cout << i << " ";
    f(i - 1);
}
```

**Call**

```cpp
f(n);
```

---

## 5. Print Numbers from **1 to N** (Using Backtracking)

### Idea

* First go till base case
* Print while returning (backtracking)

```cpp
void f(int i) {
    if (i < 1) return;

    f(i - 1);
    cout << i << " ";
}
```

**Call**

```cpp
f(n);
```

---

## 6. Print Numbers from **N to 1** (Using Backtracking)

### Idea

* Go forward first
* Print while returning

```cpp
void f(int i, int n) {
    if (i > n) return;

    f(i + 1, n);
    cout << i << " ";
}
```

**Call**

```cpp
f(1, n);
```

---

## 7. Summary Table

| Problem      | Print Position | Technique         |
| ------------ | -------------- | ----------------- |
| Name N times | Before call    | Simple recursion  |
| 1 → N        | Before call    | Forward recursion |
| N → 1        | Before call    | Reverse recursion |
| 1 → N        | After call     | Backtracking      |
| N → 1        | After call     | Backtracking      |

---

## Key Takeaways

* **Print before recursive call** → forward order
* **Print after recursive call** → backtracking
* Base condition **always mandatory**
* Backtracking = work done while returning

