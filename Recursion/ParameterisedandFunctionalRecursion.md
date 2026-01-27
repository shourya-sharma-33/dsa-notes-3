# Sum of First N Natural Numbers (Recursion)

---

## Problem
Find the **sum of first N numbers**

```

1  + 2 + 3 + ... + N

````

---

## 1. Using **Parameterised Recursion**
### Idea
- Carry the **sum as a parameter**
- Update sum at each recursive call
- Print result at base condition

👉 Yes, **we store the sum in a parameter**

### Code
```cpp
void f(int i, int sum) {
    if (i < 1) {
        cout << sum << endl;
        return;
    }
    f(i - 1, sum + i);
}
````

### Call

```cpp
f(n, 0);
```

### Flow

* `f(3,0)`
* `f(2,3)`
* `f(1,5)`
* `f(0,6)` → print `6`

---

## 2. Using **Functional Recursion** (Return Value)

### Idea

* Function **returns** the sum
* No extra parameter
* Recurrence relation

### Code

```cpp
int f(int n) {
    if (n == 0) return 0;
    return n + f(n - 1);
}
```

### Call

```cpp
cout << f(n);
```

### Flow

```
f(3)
= 3 + f(2)
= 3 + 2 + f(1)
= 3 + 2 + 1 + f(0)
= 6
```

---

## 3. Comparison

| Method        | Type         | Uses Parameter | Uses Return |
| ------------- | ------------ | -------------- | ----------- |
| Parameterised | Accumulator  | ✅ Yes          | ❌ No        |
| Functional    | Return-based | ❌ No           | ✅ Yes       |

---

## 4. Key Differences

### Parameterised Recursion

* Work done **before recursive call**
* Result available at base case
* Common in printing / accumulations

### Functional Recursion

* Work done **while returning**
* Cleaner mathematical form
* Used in DP-style thinking

---

## 5. Key Takeaways

* Both approaches are valid
* Parameterised = **carry answer**
* Functional = **build answer**
* Base condition is mandatory

---
