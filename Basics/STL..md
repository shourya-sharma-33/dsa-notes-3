# STL (Standard Template Library)

## 1. What is STL?

* STL = **Standard Template Library**
* Provides **ready-made data structures & algorithms**
* Saves time → no need to write everything from scratch
* Widely used in **DSA & Competitive Programming**

---

## 2. STL Skeleton

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    return 0;
}
```

---

## 3. STL Components

STL mainly consists of:

1. **Containers**
2. **Algorithms**
3. **Iterators**
4. **Functions**

---

## 4. Pairs

* `pair` is a container to store **two values**
* Can store **any data types**

```cpp
pair<int, int> p = {1, 3};
```

### Access

```cpp
p.first
p.second
```

### Nested Pair

```cpp
pair<int, pair<int, int>> p = {1, {2, 3}};
```

```cpp
p.second.second
```

### Array of Pairs

```cpp
pair<int, int> arr[] = {{1,2}, {2,3}, {3,4}};
```

---

## 5. Vectors

* Dynamic arrays (size can change)

```cpp
vector<int> v;
```

### Insert

```cpp
v.push_back(1);
v.emplace_back(2); // faster than push_back
```

### Initialization

```cpp
vector<int> v(5, 100); // {100,100,100,100,100}
vector<int> v(5);      // size 5, default values
```

### Copy Vector

```cpp
vector<int> v2(v);
```

### Access

```cpp
v[1];
v.at(1);
v.back();
```

---

## 6. Iterators (Vector)

```cpp
vector<int>::iterator it = v.begin();
```

* `it` points to **memory address**
* `*it` gives value
* `it++` → next element
* `it + 2` → jump 2 positions

```cpp
v.begin();  // first element
v.end();    // after last element
v.rbegin(); // last element
v.rend();   // before first element
```

---

## 7. Auto Keyword

```cpp
auto x = 4;        // int
auto it = v.begin();
```

* Compiler **automatically detects type**

---

## 8. Loops on Vector

### Iterator Loop

```cpp
for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
    cout << *it;
}
```

### Auto Iterator

```cpp
for (auto it = v.begin(); it != v.end(); it++) {
    cout << *it;
}
```

### Range-Based Loop

```cpp
for (auto it : v) {
    cout << it;
}
```

* `it` is the **value**, not iterator

---

## 9. Vector Erase

```cpp
v.erase(v.begin() + 1);
```

```cpp
v.erase(v.begin(), v.begin() + 3);
```

---

## 10. Vector Insert

```cpp
v.insert(v.begin(), 1000);
```

```cpp
v.insert(v.begin() + 1, 3, 1000); // insert 3 times
```

```cpp
v.insert(v.begin(), copy.begin(), copy.end());
```

---

## 11. Vector Utilities

```cpp
v.size();
v.pop_back();
v.clear();
v.swap(v2);
v.empty();
```

---

## 12. List

* Same usage as vector
* Allows fast insertion/deletion anywhere

```cpp
list<int> ls;
ls.push_back(2);
ls.emplace_back(4);
ls.push_front(5);
ls.emplace_front(1);
```

Functions:
`begin, end, rbegin, rend, clear, insert, size, swap`

---

## 13. Deque

* Double-ended queue

```cpp
deque<int> dq;
dq.push_back(1);
dq.push_front(2);
dq.emplace_back(3);
dq.emplace_front(4);
dq.pop_back();
dq.pop_front();
```

Supports:
`front, back, begin, end, size, clear, swap`

---

## 14. Stack

* **LIFO (Last In First Out)**

```cpp
stack<int> st;
st.push(1);
st.emplace(2);
st.top();
st.pop();
```

Utilities:
`size, empty, swap`

---

## 15. Queue

* **FIFO (First In First Out)**

```cpp
queue<int> q;
q.push(1);
q.emplace(2);
q.front();
q.back();
q.pop();
```

Utilities:
`size, empty, swap`

---

## 16. Priority Queue

* **Largest element on top (by default)**

```cpp
priority_queue<int> pq;
pq.push(5);
pq.push(1);
pq.push(10);
```

* `top()` → O(1)
* `push()` → O(log n)
* `pop()` → O(log n)

Works lexicographically for strings.

---

## 17. Set

* Stores **unique elements**
* Elements are **sorted**

```cpp
set<int> s;
s.insert(1);
s.emplace(2);
```

Functions:
`find, count, erase, begin, end, rbegin, rend, size, empty, swap`
`lower_bound, upper_bound`

---

## 18. Multiset

* Same as set
* **Allows duplicates**

```cpp
multiset<int> ms;
ms.insert(1);
ms.insert(1);
```

Functions:
`insert, erase, count, find` + all set functions

---

## 19. Unordered Set

* Stores **unique elements**
* **Not sorted**
* Faster than set (average O(1))

```cpp
unordered_set<int> us;
```

* No `lower_bound` or `upper_bound`
* Other functions same as set

---

## 20. Map

* Stores **key → value**
* Keys are **unique & sorted**

```cpp
map<int, int> mpp;
mpp[1] = 2;
```

### Traverse

```cpp
for (auto it : mpp) {
    cout << it.first << " " << it.second << endl;
}
```

### Find

```cpp
auto it = mpp.find(4);
```

Supports:
`lower_bound, upper_bound`

---

## 21. Multimap

* Same as map
* **Multiple keys allowed**
* `mpp[key]` ❌ not allowed

```cpp
multimap<int, int> mp;
```

---

## 22. Unordered Map

* Same as map
* **Not sorted**
* Faster (average O(1))

```cpp
unordered_map<int, int> ump;
```

