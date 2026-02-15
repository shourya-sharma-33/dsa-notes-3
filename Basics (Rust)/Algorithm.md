# STL Algorithms → Rust Equivalents (DSA Notes)

Rust idea:

> Most algorithms work on **slices** and **iterators**

```
&mut [T]  → sortable slice
Vec<T>    → owns data
.iter()   → read-only iterator
.iter_mut() → modifiable iterator
```

Rust uses **methods**, not free STL functions.

---

# 1. Sorting

---

## 1.1 Sorting an Array

C++:

```
sort(a, a + n);
```

Rust:

```rust
fn main() {
    let mut a = [1, 5, 3, 2];
    a.sort();
    println!("{:?}", a);
}
```

Output:

```
[1, 2, 3, 5]
```

---

## Diagram

```
[1, 5, 3, 2]
     ↓ sort
[1, 2, 3, 5]
```

Rust sorts **in-place**.

---

## Flow

```
array → mutable slice → sort()
```

Rust requires:

```
mut array
```

because sorting modifies memory.

---

## 1.2 Sorting a Vector

```rust
let mut v = vec![1, 5, 3, 2];
v.sort();
```

Works for:

✔ arrays
✔ vectors
✔ slices

Same logic everywhere.

---

## 1.3 Sorting a Subarray

Rust uses slicing syntax:

```
[start..end)
```

Same half-open rule as C++.

```rust
let mut a = [5, 2, 1, 3];
a[2..4].sort();
println!("{:?}", a);
```

Result:

```
[5, 2, 1, 3]
```

Only indexes `2, 3` sorted.

---

## Visual

```
index: 0 1 2 3
value: 5 2 1 3
            ↑↑
        sorted range
```

---

## 1.4 Descending Order

Rust uses comparator closure:

```rust
let mut a = [1, 5, 3, 2];
a.sort_by(|x, y| y.cmp(x));
```

Flow:

```
compare y to x → reverse order
```

Equivalent to C++ `greater<int>()`.

---

# 2. Custom Comparator

Rust uses closures instead of comparator functions.

---

## Thinking Model (same as C++)

You compare:

```
two elements → decide order
```

Return:

```
Ordering::Less
Ordering::Equal
Ordering::Greater
```

Rust type:

```
std::cmp::Ordering
```

---

## Example: Pair Sorting

C++ logic:

> sort by second ↑
> if equal → first ↓

Rust:

```rust
use std::cmp::Ordering;

fn main() {
    let mut v = vec![(1, 3), (2, 1), (4, 1), (3, 2)];

    v.sort_by(|a, b| {
        if a.1 < b.1 {
            Ordering::Less
        } else if a.1 > b.1 {
            Ordering::Greater
        } else {
            b.0.cmp(&a.0) // descending first
        }
    });

    println!("{:?}", v);
}
```

---

## Comparator Flow Diagram

For each pair:

```
compare second
    ↓
if equal → compare first reversed
```

Rust swaps internally just like STL.

You never touch array logic.

---

# 3. Count Set Bits

Rust equivalent of `__builtin_popcount`

---

## For integers

```rust
let x: u32 = 7; // 111
let bits = x.count_ones();
println!("{}", bits);
```

Output:

```
3
```

Works for:

```
u32, u64, i32, i64
```

---

## Mental Model

Binary:

```
7 → 111 → count 1s → 3
```

Hardware instruction optimized.

O(1).

---

# 4. Next Permutation

Rust does not have built-in `next_permutation`.

But we implement same logic easily.

---

## Idea

Rust crate exists:

```
itertools
```

But in CP, we write manual version.

---

## Printing All Permutations

Rust equivalent:

```rust
fn main() {
    let mut v = vec![1, 2, 3];
    permute(&mut v);
}

fn permute(v: &mut Vec<i32>) {
    v.sort();

    loop {
        println!("{:?}", v);
        if !next_permutation(v) {
            break;
        }
    }
}
```

---

## next_permutation Implementation

```rust
fn next_permutation(v: &mut Vec<i32>) -> bool {
    let n = v.len();

    let mut i = n - 2;
    while i < n && v[i] >= v[i + 1] {
        if i == 0 { return false; }
        i -= 1;
    }

    let mut j = n - 1;
    while v[j] <= v[i] {
        j -= 1;
    }

    v.swap(i, j);
    v[i + 1..].reverse();
    true
}
```

---

## Permutation Flow Diagram

```
123
132
213
231
312
321
```

Each step:

```
find pivot
swap
reverse suffix
```

Same algorithm as C++ STL.

---

# 5. Max / Min Element

Rust uses iterators.

---

## Maximum

```rust
let a = [1, 5, 6];
let mx = a.iter().max().unwrap();
println!("{}", mx);
```

---

## Minimum

```rust
let mn = a.iter().min().unwrap();
```

---

## Why unwrap?

Rust returns:

```
Option<&T>
```

because array could be empty.

`unwrap()` means:

> I guarantee it's not empty.

CP assumption safe.

---

## Diagram

```
[1, 5, 6]
   ↑
  max = 6
```

Iterator scans once → O(n).

---

# 6. Summary (Rust CP Algorithms)

| C++ STL            | Rust Equivalent  |     |           |
| ------------------ | ---------------- | --- | --------- |
| sort()             | slice.sort()     |     |           |
| greater<>          | sort_by(         | x,y | y.cmp(x)) |
| custom comparator  | sort_by(closure) |     |           |
| __builtin_popcount | count_ones()     |     |           |
| next_permutation   | manual function  |     |           |
| max_element        | iter().max()     |     |           |
| min_element        | iter().min()     |     |           |

---
