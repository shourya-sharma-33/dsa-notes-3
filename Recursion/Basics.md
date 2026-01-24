# Recursion – Complete Beginner Notes

## 1. Prerequisites
- Must know **what a function is**
- Able to write a simple function (e.g., add two numbers)
- Language does **not matter** (C++ / Java / Python)

---

## 2. What is Recursion?
- **Recursion** = when a **function calls itself**
- Same function exists in memory and is invoked again

**Definition**
> A function calling itself until a specified condition is met

---

## 3. Simple Recursive Call (Infinite Recursion)

```cpp
void f() {
    cout << 1 << endl;
    f();
}

int main() {
    f();
}
````

### Execution Flow

1. `main()` calls `f()`
2. `f()` prints `1`
3. `f()` calls itself again
4. Steps repeat forever

### Result

* Prints infinite `1`s
* Program crashes → **Stack Overflow**

---

## 4. Why Infinite Recursion is Dangerous?

### Stack Concept (Intuition)

* Every function call waits in **stack memory** until it finishes
* Recursive calls **do not finish immediately**
* Calls keep piling up

### Stack Overflow

* Stack has **limited memory**
* Too many waiting calls → memory exhausts
* Program crashes (segmentation fault)

---

## 5. Base Condition (Stopping Condition)

* **Base Condition** = condition where recursion stops
* Without it → infinite recursion

---

## 6. Example with Base Condition

### Goal: Print numbers from `0` to `2`

```cpp
int count = 0;

void f() {
    if (count == 3) return;   // base condition

    cout << count << endl;
    count++;
    f();
}

int main() {
    f();
}
```

### Output

```
0
1
2
```

---

## 7. How This Works (Step-by-Step)

1. `count = 0`
2. `count != 3` → print `0`, increment
3. Call `f()` again
4. Repeat until `count == 3`
5. `return` executes
6. Function calls start **unwinding**
7. Stack clears safely

---

## 8. Important Rule About `return`

* `return` **immediately terminates** the function
* No further lines execute after `return`

---

## 9. Stack Unwinding

* Recursive calls go **down**
* Base condition triggers
* Calls return **one by one**
* Stack gets cleared safely

---

## 10. Recursion Tree

* Visual representation of recursive calls
* Each node = function call
* Shows:

  * Depth of recursion
  * Order of calls and returns

Example (conceptual):

```
f()
 └── f()
      └── f()
           └── return
```

---

## 11. Key Terms Summary

### Recursion

* Function calling itself

### Infinite Recursion

* No base condition
* Leads to stack overflow

### Base Condition

* Stops recursion
* Prevents further calls

### Stack Space

* Memory holding unfinished function calls

### Stack Overflow

* Too many pending recursive calls

### Recursion Tree

* Diagrammatic view of recursive calls

---

## 12. Final Notes

* Every recursive function **must have a base condition**
* Think in terms of:

  * **Call**
  * **Stop**
  * **Return**
* Recursion = **go down + come back**

