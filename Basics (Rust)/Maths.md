
# Basic Maths (Rust Notes)

---

## 1. Digit Extraction

Given:

```
n = 7789
digits → 9, 8, 7, 7
```

---

## Diagram (Mental Model)

Think of a stack:

```
7789
 ↑
 take last digit

778
 ↑
 take last digit

77
 ↑
 take last digit
```

You are peeling digits from the right.

---

## Flow

```
step 1: digit = n % 10
step 2: n = n / 10
repeat until n == 0
```

Visual flow:

```
7789 → 778 → 77 → 7 → 0
 9      8     7    7
```

---

## Rust Code

```rust
fn main() {
    let mut n = 7789;

    while n > 0 {
        let digit = n % 10;
        println!("{}", digit);
        n /= 10;
    }
}
```

Note: Rust requires `mut` to allow modification.

---

# 2. Count Digits

## Diagram

Each division removes one digit:

```
7789 → 778 → 77 → 7 → 0
  1      2     3    4  ← count
```

---

## Flow

```
while n > 0:
    count++
    n /= 10
```

---

## Rust Code

```rust
fn count_digits(mut n: i32) -> i32 {
    let mut cnt = 0;

    while n > 0 {
        cnt += 1;
        n /= 10;
    }

    cnt
}
```

---

# 3. Reverse a Number

Goal:

```
1234 → 4321
```

---

## Diagram

```
rev = 0

take 4 → rev = 0*10 + 4 = 4
take 3 → rev = 4*10 + 3 = 43
take 2 → rev = 43*10 + 2 = 432
take 1 → rev = 432*10 + 1 = 4321
```

You are shifting left and inserting digit.

---

## Flow

```
extract digit
shift rev left (×10)
add digit
repeat
```

---

## Rust Code

```rust
fn reverse_number(mut n: i32) -> i32 {
    let mut rev = 0;

    while n > 0 {
        let ld = n % 10;
        rev = rev * 10 + ld;
        n /= 10;
    }

    rev
}
```

---

# 4. Palindrome Number

Definition:

```
original == reversed
```

Example:

```
121 → reverse → 121 ✔
123 → reverse → 321 ✘
```

---

## Flow Diagram

```
store original
reverse number
compare
```

---

## Rust Code

```rust
fn is_palindrome(n: i32) -> bool {
    let mut temp = n;
    let original = n;
    let mut rev = 0;

    while temp > 0 {
        let ld = temp % 10;
        rev = rev * 10 + ld;
        temp /= 10;
    }

    rev == original
}
```

---

# 5. Armstrong Number

Rule:

```
sum(digit^digits) == number
```

Example:

```
371 = 3³ + 7³ + 1³
```

---

## Diagram

```
digits = 3

3³ → 27
7³ → 343
1³ → 1

sum = 371
```

---

## Rust Note

Rust doesn’t use `pow()` like C++ directly for ints.
We use:

```
digit.pow(power)
```

---

## Rust Code

```rust
fn is_armstrong(mut n: i32) -> bool {
    let original = n;
    let digits = count_digits(n);
    let mut sum = 0;

    while n > 0 {
        let ld = n % 10;
        sum += ld.pow(digits as u32);
        n /= 10;
    }

    sum == original
}
```

---

# 6. Print Divisors (Brute)

## Diagram

For n = 12:

```
1 2 3 4 6 12
```

We test every number.

---

## Rust Code

```rust
fn print_divisors(n: i32) {
    for i in 1..=n {
        if n % i == 0 {
            print!("{} ", i);
        }
    }
}
```

---

# 7. Divisors Optimized (√n)

Key idea:

Divisors come in pairs:

```
i × (n/i)
```

Example:

```
2 × 6
3 × 4
```

So we only loop until √n.

---

## Diagram

```
i → pair
1 → 12
2 → 6
3 → 4
(stop after sqrt)
```

---

## Rust Code

```rust
fn divisors_optimized(n: i32) -> Vec<i32> {
    let mut divs = Vec::new();
    let mut i = 1;

    while i * i <= n {
        if n % i == 0 {
            divs.push(i);
            if n / i != i {
                divs.push(n / i);
            }
        }
        i += 1;
    }

    divs.sort();
    divs
}
```

Rust STL equivalent: `Vec` + `.sort()`.

---

# 8. Prime Check (Optimized)

Prime = no divisor except 1 & itself.

We only test until √n.

---

## Flow

```
if any i divides n → not prime
else → prime
```

---

## Rust Code

```rust
fn is_prime(n: i32) -> bool {
    if n <= 1 {
        return false;
    }

    let mut i = 2;
    while i * i <= n {
        if n % i == 0 {
            return false;
        }
        i += 1;
    }

    true
}
```

---

# 9. GCD (Brute)

We check all common divisors.

---

## Rust Code

```rust
fn gcd_brute(a: i32, b: i32) -> i32 {
    let mut ans = 1;

    for i in 1..=a.min(b) {
        if a % i == 0 && b % i == 0 {
            ans = i;
        }
    }

    ans
}
```

---

# 10. Euclidean Algorithm (Fast GCD)

Key identity:

```
gcd(a, b) = gcd(a % b, b)
```

We shrink numbers fast.

---

## Diagram

Example gcd(48,18)

```
48 % 18 = 12
18 % 12 = 6
12 % 6 = 0
answer = 6
```

---

## Rust Code

```rust
fn gcd(mut a: i32, mut b: i32) -> i32 {
    while a != 0 && b != 0 {
        if a > b {
            a %= b;
        } else {
            b %= a;
        }
    }

    if a == 0 { b } else { a }
}
```

