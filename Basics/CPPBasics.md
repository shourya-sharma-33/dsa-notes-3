
# C++ Basics

## 1. Basic Skeleton of a C++ Program

The **skeleton** of a C++ program stays almost the same across all programs.

-   `#include <iostream>` is used for input/output operations
-   `main()` is the entry point of the program
-   `std::cout` is used to print output to the console
    

```cpp
#include <iostream>
int main() {
    std::cout << "hey shourya";
    return 0;
}
```

## 2. Printing Output Multiple Times

If we print the same statement twice:

```cpp
#include <iostream>
int main() {
    std::cout << "hey shourya";
    std::cout << "hey shourya";
    return 0;
}
```

### Output

```
hey shouryahey shourya

```

This happens because there is **no newline** between the two print statements.

## 3. Using `\n` for New Line

To move output to the next line, we can use `"\n"`.

```cpp
#include <iostream>
int main() {
    std::cout << "hey shourya" << "\n";
    std::cout << "hey shourya";
    return 0;
}

```

### Output

```
hey shourya
hey shourya

```


## 4. Using `std::endl`

`std::endl` also moves the cursor to the next line (and flushes the output buffer).

```cpp
#include <iostream>
int main() {
    std::cout << "hey shourya" << std::endl
              << "meow" << std::endl
              << "meow" << std::endl
              << "meow";
    std::cout << "hey shourya";
    return 0;
}
```

### Output

```
hey shourya
meow
meow
meowhey shourya
```


## 5. Avoid Writing `std::` Again and Again

Writing `std::` every time can feel annoying. We can avoid this by using:

```cpp
using namespace std;
```

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "hey shourya";
    return 0;
}
```

 **Note:** `using namespace std;` is fine for learning and small programs, but should be avoided in large projects.


## 6. Commonly Used Libraries

-   `<iostream>` → Input / Output
-   `<cmath>` → Math functions    
-   `<string>` → String handling
    

## 7. Taking Input in C++

to take input we can do like this

```cpp
int main() {
    int x, y;
    cin >> x >> y;
    cout << "value of x is " << x << " and y is " << y;
    return 0;
}
```

-   `cin` is used to take input from the user
-   `>>` is called the extraction operator
-   input is taken in the same order as variables
    

example input:
```
5 10
```

output:
```
value of x is 5 and y is 10
```


## 8. Shortcut for Including Libraries

if u dont wanna write `#include <iostream>` and other headers everytime

u can use this instead

```cpp
#include <bits/stdc++.h>
using namespace std;
```

-   includes almost all standard C++ libraries
-   mostly used in competitive programming
-   not recommended for big projects

## 9. Data Types in C++

there are types of data  
each variable in C++ has a **data type** which decides:
- what kind of value it stores
- how much memory it uses
- its range

## int data type

used to store integers (whole numbers)

how to assign a variable:

```cpp
int x = 10;
```

range of `int` (commonly used):

-   **−2,147,483,648 to 2,147,483,647**
    
-   size: **4 bytes**
    

if value goes out of this range → overflow

## long and long long

used when numbers are **too big for int**

### long

```cpp
long x = 1000000000;
```

-   size: usually **8 bytes** (depends on system)
-   bigger range than int
    

### long long

used for **very large numbers**

```cpp
long long y = 1000000000000;
```

-   size: **8 bytes**
-   range:
    -   **−9,223,372,036,854,775,808**
    -   to **9,223,372,036,854,775,807**

mostly used in **DSA / competitive programming**


## float, double, long double

used to store **decimal values**

### float

```cpp
float x = 3.14;
```

-   size: **4 bytes**
-   precision: ~6–7 decimal digits
-   range: ~1.2e−38 to 3.4e+38
    



### double

```cpp
double y = 3.1415926535;
```

-   size: **8 bytes**
-   precision: ~15 decimal digits
-   more accurate than float
-   preferred over float
    



### long double

```cpp
long double z = 3.141592653589793238;
```

-   size: **16 bytes** (system dependent)
-   highest precision
-   used when extreme accuracy is needed
    



## char data type

used to store a **single character**

```cpp
char c = 'a';
```

-   size: **1 byte**
-   uses **single quotes**
-   can store letters, digits, symbols
    



## string data type

used to store **words or sentences**

```cpp
string s = "hello";
```

-   uses **double quotes**
-   requires `<string>` header (or bits/stdc++.h)
    



## getline (for full line input)

`cin` stops at space  
`getline` reads the **entire line**

```cpp
string s;
getline(cin, s);
```

example:
input:
```
hello world
```
output stored:
```
hello world
```

used when input contains **spaces**


# 10. If–Else and Loops in C++

## if–else statement

used to make decisions based on conditions

basic example:

```cpp
int main() {
    int age;
    cin >> age;

    if (age >= 18) {
        cout << "you are adult";
    }
    else {
        cout << "you are not adult";
    }

    return 0;
}

```

here:

-   `if` runs when condition is true
-   `else` runs when condition is false
-   conditions use operators like `> < >= <= ==`



## else if ladder

used when there are **multiple conditions**

```cpp
int main() {
    int age;
    cin >> age;

    if (age < 18) {
        cout << "not eligible";
    }
    else if (age <= 57) {
        cout << "eligible for job";

        if (age >= 55) {
            cout << " but retirement soon";
        }
    }
    else {
        cout << "retirement time";
    }

    return 0;
}
```

logic:

-   age < 18 → not eligible  
-   18 to 57 → eligible for job
-   55 to 57 → eligible but retirement soon
-   > 57 → retirement time
    

## switch case

used when checking **one variable against many fixed values**

```cpp
int main() {
    int day;
    cin >> day;

    switch(day) {
        case 1:
            cout << "Monday";
            break;
        case 2:
            cout << "Tuesday";
            break;
        case 3:
            cout << "Wednesday";
            break;
        default:
            cout << "Invalid day";
    }

    return 0;
}
```

notes:

-   `switch` works with int / char values  
-   `break` stops execution
-   `default` runs if no case matches
    

## 11. Arrays and Strings

### Array (1D array)

array is used to store **multiple values of same data type**  
indexing starts from **0**

example:

```cpp
int main() {
    int arr[5];

    cin >> arr[0] >> arr[1] >> arr[2] >> arr[3] >> arr[4];

    arr[3] = 16;   // updating value at index 3
    cout << arr[3];

    return 0;
}
```

here:

-   `arr[5]` means array of size 5  
-   valid indices: `0 to 4`
-   array values can be accessed and modified using index
    

### 2D Array

2D array is like a **matrix (rows × columns)**

syntax:

```cpp
datatype array_name[rows][cols];
```

example:

```cpp
int main() {
    int arr[2][3];

    cin >> arr[0][0] >> arr[0][1] >> arr[0][2];
    cin >> arr[1][0] >> arr[1][1] >> arr[1][2];

    cout << arr[1][2];

    return 0;
}
```

this represents:

```
row 0 → arr[0][0] arr[0][1] arr[0][2]
row 1 → arr[1][0] arr[1][1] arr[1][2]
```

used heavily in:

-   matrices
-   grids
-   DSA problems
    

### String Indexing
string is basically a **character array**

example:

```cpp
string s = "shourya";
cout << s[2];
```

output:

```
o
```

because:

```
s[0] = s
s[1] = h
s[2] = o
```

### Modifying String Characters

we can change characters using indexing

example:

```cpp
int main() {
    string s = "shourya";
    int len = s.size();

    s[len - 1] = 's';
    cout << s[len - 1];

    return 0;
}
```

here:

-   `s.size()` gives length of string  
-   last index = `len - 1`
-   strings are **mutable** in C++




## 12. Loops and Functions

### for loop

used when number of iterations is **known**

syntax:
```cpp
for(initialization; condition; update){
    // code
}

```

example:

```cpp
for(int i = 0; i < 5; i++) {
    cout << i << " ";
}

```

here:

-   initialization runs once
-   condition is checked every time
-   update runs after each iteration
    

output:

```
0 1 2 3 4

```


### while loop

used when number of iterations is **not fixed**

syntax:

```cpp
while(condition){
    // code
}

```

example:

```cpp
int i = 0;
while(i < 5) {
    cout << i << " ";
    i++;
}

```

output:

```
0 1 2 3 4

```

### do-while loop

runs **at least once**, even if condition is false

syntax:

```cpp
do {
    // code
} while(condition);

```

example:

```cpp
int i = 0;
do {
    cout << i << " ";
    i++;
} while(i < 5);

```

output:

```
0 1 2 3 4

```

important:

-   condition is checked **after** loop body
    

### infinite while loop

loop that never ends (unless broken)

```cpp
while(true) {
    cout << "looping";
}

```

used carefully with `break`


## 13. Functions in C++

function is a **block of code** that performs a task  
used to avoid repetition

syntax:

```cpp
return_type function_name(parameters){
    // code
}

```

example:

```cpp
int add(int a, int b) {
    return a + b;
}

int main() {
    cout << add(3, 4);
    return 0;
}

```

here:

-   `add` is a function 
-   takes two parameters
-   returns an int value
    
### void function

function that returns nothing

```cpp
void greet() {
    cout << "hello";
}

int main() {
    greet();
    return 0;
}

```

-
## 14. References in C++

reference is an **alias** (another name) for a variable

syntax:

```cpp
datatype &ref = variable;

```

example:

```cpp
int x = 10;
int &y = x;

y = 20;
cout << x;

```

output:

```
20

```

here:

-   `y` refers to same memory as `x`
    
-   changing `y` changes `x`
    


### Reference in Functions (Pass by Reference)

used to modify original value

```cpp
void change(int &x) {
    x = 100;
}

int main() {
    int a = 10;
    change(a);
    cout << a;
    return 0;
}

```

output:

```
100

```

important:

-   no extra copy is made  
-   faster and memory efficient
    
