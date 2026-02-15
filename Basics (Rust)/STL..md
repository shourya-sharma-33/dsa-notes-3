# Rust Collections (STL Equivalent)

## 1. Rust STL Equivalent

Rust standard collections live in:

```rust
use std::collections::*;
```

Rust gives:

* Vec → vector
* HashMap → unordered_map
* HashSet → unordered_set
* BTreeMap → sorted map
* BinaryHeap → priority queue
* VecDeque → deque

Rust is more minimal than STL — fewer containers, but powerful.

---

## 2. Pairs → Tuple

Rust doesn’t have `pair`.

It uses **tuples**.

```rust
let p = (1, 3);
```

Access:

```rust
p.0
p.1
```

Nested tuple:

```rust
let p = (1, (2, 3));
println!("{}", (p.1).1);
```

Array of tuples:

```rust
let arr = [(1,2), (2,3), (3,4)];
```

Tuples are heavily used in Rust DSA.

---

## 3. Vector → Vec

Rust vector = dynamic array.

```rust
let mut v: Vec<i32> = Vec::new();
```

Shortcut:

```rust
let mut v = vec![1, 2, 3];
```

### Insert

```rust
v.push(1);
```

Rust has no `emplace_back` — push is already efficient.

---

### Initialization

```rust
let v = vec![100; 5]; // {100,100,100,100,100}
let v = vec![0; 5];
```

---

### Copy vector

Rust default = move.

To copy:

```rust
let v2 = v.clone();
```

---

### Access

```rust
v[1]
v.get(1)   // safe option (returns Option)
v.last()
```

`get()` prevents crash.

---

## 4. Iterators

Rust is iterator-first language.

```rust
for x in &v {
    println!("{}", x);
}
```

Equivalent to STL iterator loop.

Manual iterator:

```rust
let mut it = v.iter();
println!("{:?}", it.next());
```

Rust iterators are safer than pointer iterators.

---

## 5. Auto keyword → Type inference

Rust does this automatically:

```rust
let x = 4; // compiler infers type
```

No `auto` keyword needed.

---

## 6. Loops on Vector

Range loop:

```rust
for x in &v {
    println!("{}", x);
}
```

Mutable loop:

```rust
for x in &mut v {
    *x += 1;
}
```

Index loop:

```rust
for i in 0..v.len() {
    println!("{}", v[i]);
}
```

---

## 7. Vector Erase

```rust
v.remove(1);
```

Range remove:

```rust
v.drain(0..3);
```

---

## 8. Vector Insert

```rust
v.insert(0, 1000);
```

Insert multiple:

```rust
v.splice(1..1, vec![7,8,9]);
```

---

## 9. Vector Utilities

```rust
v.len();
v.pop();
v.clear();
v.is_empty();
v.swap(0, 1);
```

Swap vectors:

```rust
std::mem::swap(&mut v1, &mut v2);
```

---

## 10. List → LinkedList

Rust has:

```rust
use std::collections::LinkedList;

let mut ls = LinkedList::new();
ls.push_back(2);
ls.push_front(1);
```

⚠️ Rarely used in DSA.

Rust prefers Vec for performance.

Same as modern C++ advice.

---

## 11. Deque → VecDeque

```rust
use std::collections::VecDeque;

let mut dq = VecDeque::new();
dq.push_back(1);
dq.push_front(2);
dq.pop_back();
dq.pop_front();
```

Perfect for BFS.

---

## 12. Stack

Rust stack = Vec

```rust
let mut st = Vec::new();

st.push(1);
st.pop();
st.last();
```

Rust doesn’t need a separate stack container.

Vec is stack.

---

## 13. Queue

Queue = VecDeque

```rust
let mut q = VecDeque::new();
q.push_back(1);
q.pop_front();
```

---

## 14. Priority Queue → BinaryHeap

```rust
use std::collections::BinaryHeap;

let mut pq = BinaryHeap::new();
pq.push(5);
pq.push(1);
pq.push(10);

println!("{:?}", pq.peek());
pq.pop();
```

Default = max heap (like C++)

Min heap:

```rust
use std::cmp::Reverse;
pq.push(Reverse(5));
```

---

## 15. Set → HashSet / BTreeSet

Unordered (fast):

```rust
use std::collections::HashSet;

let mut s = HashSet::new();
s.insert(1);
s.contains(&1);
```

Sorted:

```rust
use std::collections::BTreeSet;

let mut s = BTreeSet::new();
```

Rust splits ordered/unordered explicitly.

---

## 16. Multiset

Rust doesn’t have built-in multiset.

Common trick:

```rust
use std::collections::HashMap;

let mut ms = HashMap::new();
*ms.entry(5).or_insert(0) += 1;
```

Value = frequency.

This is how Rust handles multiset.

---

## 17. Map → HashMap / BTreeMap

Unordered:

```rust
use std::collections::HashMap;

let mut m = HashMap::new();
m.insert(1, 2);
```

Traverse:

```rust
for (k, v) in &m {
    println!("{} {}", k, v);
}
```

Find:

```rust
m.get(&1);
```

Sorted map:

```rust
use std::collections::BTreeMap;
```

---

## 18. Multimap

Rust trick:

```rust
HashMap<K, Vec<V>>
```

Example:

```rust
let mut mp: HashMap<i32, Vec<i32>> = HashMap::new();
mp.entry(1).or_default().push(5);
```

Key maps to multiple values.

---

# DSA Mapping Table

| C++ STL        | Rust          |
| -------------- | ------------- |
| vector         | Vec           |
| pair           | tuple         |
| stack          | Vec           |
| queue          | VecDeque      |
| deque          | VecDeque      |
| set            | HashSet       |
| unordered_set  | HashSet       |
| map            | HashMap       |
| unordered_map  | HashMap       |
| priority_queue | BinaryHeap    |
| multiset       | HashMap(freq) |
| multimap       | HashMap<Vec>  |

