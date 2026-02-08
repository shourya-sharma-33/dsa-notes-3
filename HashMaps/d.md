## Hashing: Basics and Motivation

### Context

This lecture introduces **basic hashing**, one of the most important topics in data structures and algorithms. Hashing is essential for solving many interview problems efficiently. The explanation uses pseudocode so the logic is language independent and can be implemented in C++, Java, Python, or any other language.

The goal is to move from brute force counting to an optimized approach.

---

## Problem Setup

Given an array:

You are repeatedly asked questions like:

: how many times does 1 appear
: how many times does 3 appear
: how many times does 2 appear
: how many times does 10 appear

Each query asks for the frequency of a number in the array.

Important observation:

: You may be asked many such queries
: The same number can be asked multiple times
: Queries can be arbitrary
: The number of queries can be very large

---

## Brute Force Approach

The most natural approach:

: For each query, scan the entire array
: Count how many times the number appears

### Pseudocode

```
function countFrequency(array, number):
    counter = 0

    for i from 0 to n - 1:
        if array[i] == number:
            counter = counter + 1

    return counter
```

### Why this works

: You iterate through every element
: Compare each element with the target number
: Increase the counter when a match is found
: Return the final counter

---

## Time Complexity Analysis

For one query:

: You traverse the full array
: Time complexity: O(n)

If you have Q queries:

: Each query costs O(n)
: Total time complexity: O(Q × n)

---

## Why This Is a Problem

Consider large constraints:

: n = 10^5
: Q = 10^5

Total operations:

: Q × n = 10^5 × 10^5 = 10^10

Performance intuition:

: 10^8 operations ≈ 1 second
: 10^10 operations ≈ 100 seconds

This is far too slow for coding interviews or competitive programming.

You cannot afford to re-scan the array for every query.

---

## Motivation for Hashing

We need:

: Faster query answering
: Avoid repeated full scans of the array
: Preprocess once, answer many times quickly

Hashing provides:

: Efficient frequency storage
: Near constant time lookup
: Dramatic performance improvement

Instead of recomputing counts every time, hashing stores frequencies in advance and answers each query in O(1) on average.

---

## Key Idea Behind Hashing

: Precompute frequency of every number
: Store counts in a hash structure
: Answer queries using direct lookup

This shifts the cost:

: One-time preprocessing: O(n)
: Each query: O(1) average
: Total: O(n + Q)

Much better than O(Q × n).

---

## Code Example

### `input`

```
5
1 3 2 1 3
5
1
4
2
3
12
```

### code

```cpp
int main()
{
    int n;
    cin>>n;
    int arr[n];
    for (int i=0; i<n; i++)
    {
        cin>>arr[i];
    }

    // precompute
    int hash[13] = (0);
    for (int i =0; i<n; i++)
    {
        hash[arr[i]] += 1;
    }

    int q;
    cin>>q;
    while(q--)
    {
        int number;
        cin>>number;
        cout<<hash[number]<<endl;
    }

    return 0;
}
```

## Hashing: Core Idea

### Naive definition

Hashing can be understood simply as:

: pre storing
: fetching when required

You store useful information in advance and later retrieve it instantly instead of recomputing.

---

## Number Hashing with Arrays

### Problem assumption

We are given an array whose elements are bounded.

Example:

: maximum possible value in the array is 12

Even if current elements are small, we know the upper limit.

Example array:

```
1 2 1 3 2
```

---

### Creating a hash array

If maximum value = 12:

: we create an array of size 13
: indices go from 0 to 12
: initialize everything to 0

This array is called:

: hash array
: frequency array

---

### Precomputation step

We traverse the original array once.

For each element:

```
hash[array[i]]++
```

Example result:

: hash[1] = 2
: hash[2] = 2
: hash[3] = 1
: others = 0

This is the pre storing phase.

---

### Fetching answers

To answer queries:

: how many times does 1 appear → hash[1]
: how many times does 4 appear → hash[4]
: how many times does 12 appear → hash[12]

Each query is answered in O(1).

No full array scan is needed.

---

### Full flow

Input:

: array size n
: array elements
: number of queries q
: q numbers to query

Steps:

: build hash array using one loop → O(n)
: answer each query using lookup → O(1) per query

Total time:

: O(n + q)

---

## Memory Limitations of Array Hashing

Array hashing only works when values are small.

If max value is:

: 10^9
: 10^12
: 10^18

You cannot create arrays of that size.

Practical limits in C++:

Inside main:

: integer array ≈ up to 10^6

Globally declared:

: integer array ≈ up to 10^7

Boolean arrays allow slightly larger sizes.

Beyond that:

: segmentation fault
: memory allocation failure

So array hashing is not suitable for huge numeric ranges.

---

## Character Hashing

### Problem

Given a string and many queries:

: how many times does a character appear

Example string:

```
abcdabefc
```

---

### Brute force

For each query:

: scan full string
: count matches

Time complexity:

: O(q × n)

Too slow for large inputs.

---

### Hashing lowercase characters

Assume only lowercase letters:

: total possible characters = 26
: a to z

We create:

```
hash[26]
```

Mapping rule:

```
index = character - 'a'
```

Why this works:

: ASCII('a') = 97
: ASCII('b') = 98

So:

: 'a' - 'a' = 0
: 'b' - 'a' = 1
: 'c' - 'a' = 2

---

### Precomputation

```
for each character ch in string:
    hash[ch - 'a']++
```

### Query

```
answer = hash[c - 'a']
```

---

## Hashing all characters

If string can contain any character:

: ASCII range ≈ 256

We create:

```
hash[256]
```

Then simply:

```
hash[ch]++
```

Characters auto convert to ASCII integers.

No subtraction needed.

Character hashing is safe because:

: 256 is small
: arrays easily support it

---

## When Arrays Are Not Enough: Map Hashing

If numbers are huge:

: 10^9
: 10^12
: sparse values

We use maps instead of arrays.

```
abcdabehf
5
a
g
h
b
c
```

```cpp
int main()
{
    string s;
    cin>>s;

    int hash[256] = 0;
    for (int i =0; i<s.size(); i++)
    {
        hash[s[i]]++;
    }
    int q;
    cin>>q;
    while(q--)
    {
        char c;
        cin>>c;
        cout<<hash[c]<<endl;
    }
    return 0;
}
```
---



## Map Concept

A map stores:

: key → value

For frequency counting:

: key = number
: value = frequency

Example array:

```
1 2 3 1 3 2
```

We do:

```
map[array[i]]++
```

Result:

: 1 → 2
: 2 → 2
: 3 → 2

Only existing elements are stored.

Unlike arrays:

: no wasted space
: no need for huge size allocation

---

### Fetching

```
map[x]
```

If x is not present:

: map returns 0
: does not store unnecessary entries

---

### Properties of map

In C++ map:

: keys stored in sorted order
: internally balanced tree
: slightly slower than array
: memory efficient for sparse data

---

### Character hashing using map

We can also do:

```
map<char, int> freq
freq[ch]++
```

Works like array hashing but dynamic.

---

## Summary

Array hashing:

: fastest lookup
: best for small bounded ranges

Character hashing:

: use size 26 or 256 arrays
: always safe

Map hashing:

: works for huge numbers
: stores only required keys
: memory efficient
: slightly slower than arrays

---

## Map vs Unordered Map: Time Complexity

### Time complexity of map

In a standard ordered map (C++ `map`):

: storing a value → O(log n)
: fetching a value → O(log n)

This holds in:

: best case
: average case
: worst case

Always logarithmic.

Reason:

: internally implemented using balanced binary search tree
: elements are kept sorted
: tree height ≈ log n

So every operation travels tree height → log n.

---

## Unordered Map

`unordered_map` is based on hashing.

Key idea:

: no sorting
: direct bucket access using hash function

### Time complexity

Average case:

: store → O(1)
: fetch → O(1)

Best case:

: O(1)

Worst case:

: O(n)

Worst case happens when many elements collide into the same bucket.

In practice:

: average O(1) almost always
: worst case is rare
: used in competitive programming by default

Rule of thumb:

: prefer unordered_map first
: switch to map only if needed

---

## Why worst case happens: collisions

A collision means:

: multiple keys map to the same hash index

Then elements must be stored in a chain.

If a chain becomes very long:

: search becomes linear
: complexity degrades to O(n)

---

## Division method intuition

To understand collisions, imagine:

You are allowed an array of size 10 only:

```
index: 0 1 2 3 4 5 6 7 8 9
```

Hash function:

```
index = value % 10
```

Example numbers:

```
2 5 16 28 139
```

Mapping:

: 2 % 10 = 2
: 5 % 10 = 5
: 16 % 10 = 6
: 28 % 10 = 8
: 139 % 10 = 9

So we store counts at those indices.

```
7
1 2 3 1 3 2 12
5
1
2
3
4
12
```

```cpp
int main()
{
    int n;
    cin>>n;
    int arr[n];
    for(int i = 0; i<n; i++)
    {
        cin>>arr[i];
    }
    map<int, int>mpp;
    for (int i = 0; i<n; i++)
    {
        mpp[arr[i]]++;
    }

    int q;
    cin>>q;
    while(q--)
    {
        int number;
        cin>>numbers;
        cout<<app(number)<<endl;
    }
    return 0;
}
```

```cpp
int main()
{
    int n;
    cin>>n;
    map<int, int>mpp;
    int arr[n];
    for(int i = 0; i<n; i++)
    {
        cin>>arr[i];
        mpp[arr[i]]++;
    }

    for(auto it : mpp)
    {
        cout<<it.first<< "->" << it.second <<endl;
    }

    int q;
    cin>>q;
    while(q--)
    {
        int number;
        cin>>numbers;
        cout<<app(number)<<endl;
    }
    return 0;
}
```
---

### Collision example

Now consider:

```
18 28 38 48
```

All map to:

```
value % 10 = 8
```

So bucket 8 gets a chain:

```
8 → 18 → 28 → 38 → 48
```

Everyone collided.

This is collision.

If chain becomes huge:

: lookup becomes slow
: linear search inside chain
: worst case O(n)

That is exactly unordered_map worst case.

---

## Why worst case is rare

Real hash tables:

: use better hash functions
: resize dynamically
: distribute keys well

So all elements landing in the same bucket is extremely unlikely.

That is why unordered_map is fast in practice.

---

## Map vs Unordered Map Summary

map:

: sorted order
: tree based
: O(log n) always
: stable performance

unordered_map:

: no order
: hash based
: average O(1)
: worst O(n)
: fastest in practice

Use unordered_map by default.

---

## Key types

map supports:

: int
: double
: char
: string
: pair
: vector
: custom structures

unordered_map supports common primitive keys easily:

: int
: double
: char
: string

Complex keys require custom hash functions.

---

## Interview takeaway

If asked complexity:

unordered_map:

: average O(1)
: worst O(n) due to collisions

map:

: O(log n) guaranteed

This answer is enough for interviews.

---
