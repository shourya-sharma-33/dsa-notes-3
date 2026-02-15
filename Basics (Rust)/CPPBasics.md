Perfect — I’ll convert this into **Rust DSA starter notes**, matching your structure and intent.
I’ll keep your mental model intact and point out where Rust differs.

---

# Rust Basics (C++ → Rust Translation)

Rust is stricter than C++ but safer.
No undefined behavior, no garbage memory, no silent bugs.

Think of Rust as:

> C++ + safety + strict rules + modern syntax

---

## 1. Basic Skeleton of a Rust Program

Rust does not use headers like C++.

Everything starts with `fn main()`.

```rust
fn main() {
    println!("hey shourya");
}
```

### Key differences

* no `#include`
* `println!` is a macro (notice the `!`)
* semicolon ends statements
* no `return 0;` needed

Rust automatically returns success from `main`.

---

## 2. Printing Output Multiple Times

```rust
fn main() {
    print!("hey shourya");
    print!("hey shourya");
}
```

Output:

```
hey shouryahey shourya
```

Same behavior as C++ — no newline.

---

## 3. New Line Printing

Rust equivalent of `\n` or `endl`:

```rust
fn main() {
    println!("hey shourya");
    println!("hey shourya");
}
```

Each `println!` automatically adds a newline.

You can also manually:

```rust
print!("hello\n");
```

---

## 4. No `using namespace std`

Rust does not need this.

Everything from standard library is already available.

Cleaner than C++.

---

## 5. Taking Input in Rust

Rust input is slightly more verbose, but safe.

```rust
use std::io;

fn main() {
    let mut input = String::new();

    io::stdin()
        .read_line(&mut input)
        .expect("failed");

    let x: i32 = input.trim().parse().expect("not a number");

    println!("value of x is {}", x);
}
```

### Explanation

* `let mut` → mutable variable
* `String::new()` → empty string
* `read_line` reads input
* `trim()` removes newline
* `parse()` converts string → number

Rust forces safe parsing.

No silent failures.

---

## 6. Data Types in Rust

Rust uses **explicit integer sizes**.

### Integer types

```rust
let x: i32 = 10;   // like C++ int
let y: i64 = 10000000000; // like long long
```

Common types:

| Rust  | Meaning                           |
| ----- | --------------------------------- |
| i32   | 32-bit integer                    |
| i64   | 64-bit integer                    |
| usize | index type (important for arrays) |

For DSA:

👉 use **i64** when numbers are big
👉 use **usize** for indexing

---

### Floating point

```rust
let a: f32 = 3.14;
let b: f64 = 3.141592;
```

`f64` is default (like C++ double).

---

### Character

```rust
let c: char = 'a';
```

Rust chars are Unicode — bigger than C++ char.

---

### String

Rust has **two string types**

#### &str (string slice) — immutable

```rust
let s = "hello";
```

#### String — growable

```rust
let mut s = String::from("hello");
```

For DSA → use `String`

---

## 7. Full Line Input (getline equivalent)

```rust
use std::io;

fn main() {
    let mut s = String::new();
    io::stdin().read_line(&mut s).unwrap();

    println!("{}", s.trim());
}
```

Equivalent of C++ `getline`.

---

## 8. If–Else in Rust

Same logic, cleaner syntax.

```rust
fn main() {
    let age = 20;

    if age >= 18 {
        println!("adult");
    } else {
        println!("not adult");
    }
}
```

No parentheses needed around condition.

---

### else if ladder

```rust
if age < 18 {
    println!("not eligible");
} else if age <= 57 {
    println!("eligible");
} else {
    println!("retirement");
}
```

Same logic as C++.

---

## 9. Match (switch case equivalent)

Rust uses `match`.

```rust
let day = 2;

match day {
    1 => println!("Monday"),
    2 => println!("Tuesday"),
    3 => println!("Wednesday"),
    _ => println!("Invalid"),
}
```

`_` = default case.

Rust match is safer than switch.

---

## 10. Arrays

Fixed-size array:

```rust
let arr = [1, 2, 3, 4, 5];
println!("{}", arr[3]);
```

Index starts at 0.

Rust checks bounds at runtime:

👉 invalid index = program crash
(no silent garbage memory like C++)

---

### 2D Array

```rust
let arr = [[1, 2, 3], [4, 5, 6]];
println!("{}", arr[1][2]);
```

Used for grids and matrices.

---

## 11. Strings and Indexing

Rust strings are UTF-8.

Direct indexing is tricky.

Instead:

```rust
let s = String::from("hello");
let bytes = s.as_bytes();

println!("{}", bytes[1] as char);
```

For DSA, we often convert:

```rust
let chars: Vec<char> = s.chars().collect();
println!("{}", chars[1]);
```

This is Rust’s safe way.

---

## 12. Loops

### for loop

```rust
for i in 0..5 {
    print!("{} ", i);
}
```

`0..5` means 0 to 4.

---

### while loop

```rust
let mut i = 0;
while i < 5 {
    print!("{} ", i);
    i += 1;
}
```

---

### infinite loop

```rust
loop {
    println!("running");
    break;
}
```

Rust keyword: `loop`

---

## 13. Functions

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn main() {
    println!("{}", add(3, 4));
}
```

Key rule:

👉 last line without semicolon = return value

---

### void function

Rust equivalent:

```rust
fn greet() {
    println!("hello");
}
```

Return type = `()`

(unit type)

---

## 14. References (VERY IMPORTANT IN RUST)

Rust references are like C++, but safer.

```rust
fn change(x: &mut i32) {
    *x = 100;
}

fn main() {
    let mut a = 10;
    change(&mut a);
    println!("{}", a);
}
```

Rules:

* `&` = borrow
* `&mut` = mutable borrow
* `*x` = dereference

Rust enforces:

👉 no data races
👉 no dangling references
👉 safe memory

---

This is your **C++ → Rust mental bridge**.

You now understand Rust basics in DSA terms.

---

Next step options:

✅ Rust vectors (C++ vector equivalent)
✅ HashMap / HashSet (STL containers)
✅ Rust ownership simplified for DSA
✅ Iterators
✅ Competitive programming Rust template

Tell me what to translate next. 🚀
