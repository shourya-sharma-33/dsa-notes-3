# Rooms and Staircases: Codeforces Round 592 (Div. 2)

## Problem Overview

We are given a house with:
two floors
n rooms on each floor
rooms are numbered from 1 to n on both floors

Movement rules:
you can move left or right on the same floor between adjacent rooms
you can move between floors only if a staircase exists at that room index
you cannot visit the same room twice

Input representation:
a string of length n made of 0 and 1
0 means no staircase at that index
1 means a staircase exists connecting both floors at that index

Goal:
find the maximum number of distinct rooms Nikolay can visit
he can start from any room on any floor

---

## Key Observations

1: Total rooms = 2 * n
2: Without staircases, you can only traverse one floor completely
maximum = n

3: Staircases allow switching floors and extending traversal
4: The best strategy is to walk in one direction and use staircases optimally
5: If we ever use a staircase at index i:
we can potentially cover both floors up to that index
rooms covered = 2 * (i + 1)

6: Even without switching, we can still count linear traversal on one floor

7: Direction matters:
sometimes starting from left gives best result
sometimes starting from right gives best result
so we must evaluate both directions

---

## Core Idea

For a given direction:
maintain a running count of rooms visited on one floor
when we encounter a '1', we can switch floors and potentially double coverage

Answer is the maximum of:
normal traversal count
2 * (index + 1) when staircase is available

Repeat the same logic from reverse direction

---

## Algorithm Steps

1: Initialize answer = n
2: Traverse string from left to right
3: Count rooms visited normally
4: If s[i] == '1', update answer using 2 * (i + 1)
5: Update answer with normal traversal count
6: Reverse the string
7: Repeat steps 2 to 5
8: Output final answer

---

## C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve() {
    int n;
    cin >> n;
    string s;
    cin >> s;

    int ans = n;

    for (int pass = 0; pass < 2; pass++) {
        int c = 0;
        for (int i = 0; i < n; i++) {
            c++;
            if (s[i] == '1') {
                ans = max(ans, 2 * (i + 1));
                c++;
            }
        }
        ans = max(ans, c);
        reverse(s.begin(), s.end());
    }

    cout << ans << endl;
}

int main() {
    int t;
    cin >> t;
    while (t--) {
        solve();
    }
    return 0;
}
```

---

## Intuition Summary

Think of the problem as:
how far can I go in one direction
and when can I double my progress using staircases

This problem teaches:
observing input behavior
thinking in terms of traversal patterns
reducing a seemingly complex graph problem into simple linear scans

Very common Codeforces style insight problem.
