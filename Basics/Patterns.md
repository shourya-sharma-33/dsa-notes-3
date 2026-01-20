

# Nested Loop Patterns (C++ Notes)

---

## 1. Solid Rectangle

### Pattern

```
******
******
******
******
```

### Explanation

* Rows = 4
* Columns = 6
* Same number of symbols in every row

### Intuition

* Outer loop → rows
* Inner loop → fixed columns

### Code

```cpp
for (int i = 0; i < 4; i++) {
    for (int j = 0; j < 6; j++) {
        cout << "*";
    }
    cout << endl;
}
```

---

## 2. Increasing Triangle

### Pattern

```
x
xx
xxx
xxxx
xxxxx
```

### Explanation

* Rows = 5
* Columns increase with row number

### Intuition

* Inner loop runs till `i`

### Code

```cpp
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        cout << "x";
    }
    cout << endl;
}
```

---

## 3. Decreasing Triangle

### Pattern

```
xxxxxx
xxxxx
xxxx
xxx
xx
x
```

### Explanation

* Rows decrease from 6 to 1

### Intuition

* Outer loop controls size
* Inner loop runs till current row value

### Code

```cpp
for (int i = 6; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        cout << "x";
    }
    cout << endl;
}
```

---

## 4. Symmetric Triangle (Line of Symmetry)

### Pattern

```
x
xx
xxx
xxxx
xxxxx
xxxxxx
xxxxx
xxxx
xxx
xx
x
```

### Explanation

* First half → increasing
* Second half → decreasing

### Intuition

* Symmetry breaks at the middle line

### Code

```cpp
int n = 6;

// increasing
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) cout << "x";
    cout << endl;
}

// decreasing
for (int i = n - 1; i >= 1; i--) {
    for (int j = 1; j <= i; j++) cout << "x";
    cout << endl;
}
```

---

## 5. Binary Triangle (Flip Variable)

### Pattern

```
1
01
101
0101
10101
```

### Explanation

* Each row alternates between `0` and `1`

### Intuition

* Use a variable
* Flip after every print

### Code

```cpp
for (int i = 1; i <= 5; i++) {
    int val = i % 2;
    for (int j = 1; j <= i; j++) {
        cout << val;
        val = 1 - val;
    }
    cout << endl;
}
```

---

## 6. Number Palindrome Pyramid

### Pattern

```
1      1
12    21
123  321
12344321
```

### Explanation

* Left numbers increase
* Right numbers decrease
* Spaces in between

### Intuition

* Number loop
* Space loop
* Reverse number loop

### Code

```cpp
int n = 4;
for (int i = 1; i <= n; i++) {

    for (int j = 1; j <= i; j++) cout << j;

    for (int s = 1; s <= 2*(n - i); s++) cout << " ";

    for (int j = i; j >= 1; j--) cout << j;

    cout << endl;
}
```

---

## 7. Continuous Numbers Triangle

### Pattern

```
1
2 3
4 5 6
7 8 9 10
11 12 13 14 15
```

### Explanation

* Numbers continue across rows

### Intuition

* Maintain a running counter

### Code

```cpp
int num = 1;
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        cout << num++ << " ";
    }
    cout << endl;
}
```

---

## 8. Alphabet Increasing Triangle

### Pattern

```
A
A B
A B C
A B C D
A B C D E
```

### Explanation

* Characters increase till row length

### Intuition

* Start from `'A'` every row

### Code

```cpp
for (int i = 1; i <= 5; i++) {
    char ch = 'A';
    for (int j = 1; j <= i; j++) {
        cout << ch++ << " ";
    }
    cout << endl;
}
```

---

## 9. Same Character Triangle

### Pattern

```
A
B B
C C C
D D D D
E E E E E
```

### Explanation

* Same character repeated per row

### Intuition

* Character depends only on row

### Code

```cpp
char ch = 'A';
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        cout << ch << " ";
    }
    ch++;
    cout << endl;
}
```

---

## 10. Alphabet Pyramid

### Pattern

```
    A
   ABC
  ABCDE
 ABCDEFG
ABCDEFGHI
```

### Explanation

* Center aligned
* Characters increase

### Intuition

* Spaces = `n - i`
* Characters = `2*i - 1`

### Code

```cpp
int n = 5;
for (int i = 1; i <= n; i++) {

    for (int s = 1; s <= n - i; s++) cout << " ";

    char ch = 'A';
    for (int j = 1; j <= 2*i - 1; j++) cout << ch++;

    cout << endl;
}
```

---

## 11. Palindrome Alphabet Pyramid

### Pattern

```
    A
   ABA
  ABCBA
 ABCDCBA
ABCDEDCBA
```

### Explanation

* Left side increasing
* Right side decreasing

### Intuition

* Split pyramid into two halves

### Code

```cpp
int n = 5;
for (int i = 1; i <= n; i++) {

    for (int s = 1; s <= n - i; s++) cout << " ";

    char ch = 'A';
    for (int j = 1; j <= i; j++) cout << ch++;

    ch -= 2;
    for (int j = 1; j < i; j++) cout << ch--;

    cout << endl;
}
```

---

## 12. Hollow X Pattern

### Pattern

```
*********
**** ****
***   ***
**     **
*       *
**     **
***   ***
**** ****
*********
```

### Explanation

* Hollow center
* Symmetric on both sides

### Intuition

* Print stars only on boundaries

### Code

```cpp
int n = 5;
for (int i = n; i >= 1; i--) {
    for (int j = 1; j <= i; j++) cout << "*";
    for (int s = 1; s <= 2*(n - i); s++) cout << " ";
    for (int j = 1; j <= i; j++) cout << "*";
    cout << endl;
}

for (int i = 2; i <= n; i++) {
    for (int j = 1; j <= i; j++) cout << "*";
    for (int s = 1; s <= 2*(n - i); s++) cout << " ";
    for (int j = 1; j <= i; j++) cout << "*";
    cout << endl;
}
```

---

## 13. Hollow Square

### Pattern

```
****
*  *
*  *
****
```

### Explanation

* Border stars only

### Intuition

* Print star if on boundary

### Code

```cpp
int n = 4;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
        if (i == 1 || i == n || j == 1 || j == n)
            cout << "*";
        else
            cout << " ";
    }
    cout << endl;
}
```

---

## 14. Number Square Pattern

### Pattern

```
4444444
4333334
4322234
4321234
4322234
4333334
4444444
```

### Explanation

* Numbers decrease towards center

### Intuition

* Value depends on minimum distance from borders

### Code

```cpp
int n = 4;
for (int i = 0; i < 2*n-1; i++) {
    for (int j = 0; j < 2*n-1; j++) {
        int val = n - min(min(i, j), min(2*n-2-i, 2*n-2-j));
        cout << val;
    }
    cout << endl;
}
```

