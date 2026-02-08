# Merge Sort Notes

## Definition

Merge sort is a divide and conquer sorting algorithm.

It repeatedly divides an array into smaller halves, sorts each half, and then merges the sorted halves back together.

---

## Core Idea

Merge sort works in two phases:

Divide:
Split the array into halves until each subarray has one element

Merge:
Combine subarrays back together in sorted order

A single element array is already sorted.

---

## Steps of Merge Sort

1. Divide the array into two halves
2. Recursively apply merge sort to each half
3. Merge the two sorted halves into one sorted array

This continues until the entire array becomes sorted.

---

## Merge Operation

To merge two sorted arrays:

1. Use two pointers, one for each array
2. Compare elements at both pointers
3. Insert the smaller element into a temporary array
4. Move the pointer of the chosen element
5. Repeat until one array is exhausted
6. Copy remaining elements from the other array

---

## Base Case

Stop recursion when:

low >= high

This means the subarray has one or zero elements.

---

## Pseudocode Structure

```
mergeSort(arr, low, high):
    if low >= high: return

    mid = (low + high) / 2

    mergeSort(arr, low, mid)
    mergeSort(arr, mid+1, high)

    merge(arr, low, mid, high)
```

---

## Time Complexity

Best case: O(n log n)
Average case: O(n log n)
Worst case: O(n log n)

Reason:
Array splits log n times
Each merge takes O(n)

Total = n log n

---

## Space Complexity

O(n)

Because we use a temporary array during merging.

---

## Properties

Stable sort: yes
In-place: no
Comparison-based: yes
Recursive: yes

---

# Example

Sort this array:

```
[5, 2, 4, 1, 3]
```

---

## Divide Phase

```
[5,2,4,1,3]
→
[5,2,4]   [1,3]
→
[5] [2,4] [1] [3]
→
[5] [2] [4] [1] [3]
```

All single elements → stop dividing

---

## Merge Phase

Merge [2] and [4]:

```
[2,4]
```

Merge [5] and [2,4]:

```
[2,4,5]
```

Merge [1] and [3]:

```
[1,3]
```

Final merge:

Left:  [2,4,5]
Right: [1,3]

Steps:

1 vs 2 → 1
2 vs 3 → 2
4 vs 3 → 3
remaining → 4,5

Result:

```
[1,2,3,4,5]
```


# Code

```cpp
#include <bits/stdc++.h>
using namespace std;

void mergeArray(vector<int>& arr, int low, int mid, int high) {
    vector<int> temp;
    int left = low;
    int right = mid + 1;

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push_back(arr[left]);
            left++;
        } else {
            temp.push_back(arr[right]);
            right++;
        }
    }

    while (left <= mid) {
        temp.push_back(arr[left]);
        left++;
    }

    while (right <= high) {
        temp.push_back(arr[right]);
        right++;
    }

    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }
}

void mergeSort(vector<int>& arr, int low, int high) {
    if (low >= high) return;

    int mid = (low + high) / 2;
    mergeSort(arr, low, mid);
    mergeSort(arr, mid + 1, high);
    mergeArray(arr, low, mid, high);
}

int main() {
    int n;
    cin >> n;

    vector<int> arr(n);
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    mergeSort(arr, 0, n - 1);

    for (int x : arr) {
        cout << x << " ";
    }

    return 0;
}
```

Example input:

```
5
5 2 4 1 3
```

Example output:

```
1 2 3 4 5
```
