# Quick Sort

## Overview

Quick sort is a divide and conquer sorting algorithm that sorts an array in ascending order. With minor tweaks, it can also sort in descending order.

It has:

Time complexity: O(n log n) average
Worst case: O(n²)
Space complexity: O(1) extra space (ignoring recursion stack)

Unlike merge sort, quick sort does not use a temporary array.

---

## Core Idea

Quick sort repeatedly:

1. Picks a pivot
2. Places the pivot in its correct sorted position
3. Moves smaller elements to the left of pivot
4. Moves larger elements to the right of pivot
5. Recursively sorts left and right parts

Any element can be chosen as pivot:

first element
last element
middle element
random element

In this explanation, pivot = first element.

---

## Algorithm Intuition

If a pivot is placed at its correct sorted index:

All elements on the left must be smaller
All elements on the right must be larger

After placing one pivot correctly, the problem splits into two smaller unsorted subarrays.

This is recursion.

---

## Partition Logic

We maintain:

low pointer: start of subarray
high pointer: end of subarray
pivot = array[low]

We use two pointers:

i: moves from left
j: moves from right

Steps:

Move i until element > pivot
Move j until element < pivot

If i < j: swap them
Repeat until i ≥ j

Finally:

swap pivot with array[j]

Now pivot is at correct index
j becomes partition index

---

## Recursive Structure

After partition:

left subarray: low → partitionIndex − 1
right subarray: partitionIndex + 1 → high

Apply quick sort recursively on both.

Base condition:

If low ≥ high: stop
Single element arrays are already sorted

---

## Pseudocode

```
quickSort(arr, low, high):
    if low < high:
        p = partition(arr, low, high)
        quickSort(arr, low, p-1)
        quickSort(arr, p+1, high)
```

```
partition(arr, low, high):
    pivot = arr[low]
    i = low
    j = high

    while i < j:
        while arr[i] <= pivot and i <= high-1:
            i++

        while arr[j] > pivot and j >= low+1:
            j--

        if i < j:
            swap(arr[i], arr[j])

    swap(arr[low], arr[j])
    return j
```

---

## Why It Works

Each partition step:

Places one element in final sorted position
Splits problem into two smaller independent problems
Eventually reduces to size 1 arrays

That guarantees full sorting.

---

## Time Complexity

Best case: O(n log n)
Average case: O(n log n)
Worst case: O(n²)

Worst case happens when pivot is always smallest or largest element
Example: already sorted array with bad pivot choice

---

## Space Complexity

Extra array: none
In-place sorting: yes
Auxiliary space: O(1)

Recursion stack: O(log n) average


--- 

We’ll use this array:

Array: `[4, 6, 2, 5, 7, 9, 1, 3]`
Pivot rule: first element

---

# Example Walkthrough

## Step 1: First partition

Array: `[4, 6, 2, 5, 7, 9, 1, 3]`
pivot = 4

Goal:
smaller left of 4
larger right of 4

We rearrange:

`[3, 1, 2, 4, 7, 9, 5, 6]`

Pivot 4 is now in its correct sorted position.

Left part: `[3, 1, 2]`
Right part: `[7, 9, 5, 6]`

---

## Step 2: Sort left part `[3, 1, 2]`

pivot = 3

Partition:

`[2, 1, 3]`

Pivot 3 is fixed.

Now sort `[2, 1]`

pivot = 2

Partition:

`[1, 2]`

Left side fully sorted.

So left half becomes:

`[1, 2, 3]`

---

## Step 3: Sort right part `[7, 9, 5, 6]`

pivot = 7

Partition:

`[6, 5, 7, 9]`

Pivot 7 fixed.

Sort left `[6, 5]`

pivot = 6

Partition:

`[5, 6]`

Right `[9]` is already sorted.

So right half becomes:

`[5, 6, 7, 9]`

---

## Final array

Combine everything:

`[1, 2, 3, 4, 5, 6, 7, 9]`

Sorted ✅

---

# Recursion Tree View

```
[4 6 2 5 7 9 1 3]
        4
   /           \
[3 1 2]     [7 9 5 6]
   3            7
 /   \        /     \
[2 1] []   [6 5]    [9]
 2            6
/ \          / \
1  2        5  6
```

Each pivot locks into final position.

# Code 
```cpp
#include <bits/stdc++.h>
using namespace std;

int partitionArray(vector<int>& arr, int low, int high) {
    int pivot = arr[low];
    int i = low;
    int j = high;

    while (i < j) {
        while (i <= high - 1 && arr[i] <= pivot) i++;
        while (j >= low + 1 && arr[j] > pivot) j--;

        if (i < j) swap(arr[i], arr[j]);
    }

    swap(arr[low], arr[j]);
    return j;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int p = partitionArray(arr, low, high);
        quickSort(arr, low, p - 1);
        quickSort(arr, p + 1, high);
    }
}

int main() {
    int n;
    cin >> n;

    vector<int> arr(n);
    for (int i = 0; i < n; i++) cin >> arr[i];

    quickSort(arr, 0, n - 1);

    for (int x : arr) cout << x << " ";

    return 0;
}
```

Example input:

```
8
4 6 2 5 7 9 1 3
```

Example output:

```
1 2 3 4 5 6 7 9
```
