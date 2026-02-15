# Pattern Thinking (Core Idea)

Every nested loop pattern is:

```
row loop → controls height
column loop → controls what prints in that row
```

Think in table form:

```
i = row number
j = column number
```

You are drawing pixels row by row.

---

# 1. Solid Rectangle

## Diagram

Each row prints 6 stars.

```
Row 1 → ******
Row 2 → ******
Row 3 → ******
Row 4 → ******
```

Grid view:

```
i=1  * * * * * *
i=2  * * * * * *
i=3  * * * * * *
i=4  * * * * * *
      ↑
      j runs 6 times
```

---

## Flow Explanation

For every row:

👉 inner loop prints 6 stars
👉 move to next line
👉 repeat 4 times

Flow:

```
i = 1
  j: ******

i = 2
  j: ******

i = 3
  j: ******

i = 4
  j: ******
```

Columns do NOT depend on row → fixed rectangle.

---

## Rust Code

```rust
fn main() {
    for _ in 0..4 {        // rows
        for _ in 0..6 {    // columns
            print!("*");
        }
        println!();
    }
}
```

---

# 2. Increasing Triangle

## Diagram

Each row prints equal to row number.

```
Row 1 → x
Row 2 → xx
Row 3 → xxx
Row 4 → xxxx
Row 5 → xxxxx
```

Table view:

```
i=1  x
i=2  x x
i=3  x x x
i=4  x x x x
i=5  x x x x x
```

---

## Flow Explanation

Inner loop depends on `i`.

```
i = 1 → j runs 1 time
i = 2 → j runs 2 times
i = 3 → j runs 3 times
...
```

So row length grows with i.

Mental rule:

> print i characters in row i

---

## Rust Code

```rust
fn main() {
    for i in 1..=5 {
        for _ in 1..=i {
            print!("x");
        }
        println!();
    }
}
```

---

# 3. Decreasing Triangle

## Diagram

Reverse of previous:

```
xxxxxx
xxxxx
xxxx
xxx
xx
x
```

Table:

```
i=6  x x x x x x
i=5  x x x x x
i=4  x x x x
...
```

---

## Flow Explanation

Now rows shrink.

```
i = 6 → j runs 6 times
i = 5 → j runs 5 times
...
```

Mental rule:

> print i characters while i decreases

---

## Rust Code

```rust
fn main() {
    for i in (1..=6).rev() {
        for _ in 1..=i {
            print!("x");
        }
        println!();
    }
}
```

`.rev()` = reverse iteration.

---

# 4. Symmetric Triangle

This is just:

```
increasing triangle
+
decreasing triangle
```

## Diagram

```
x
xx
xxx
xxxx
xxxxx
xxxxxx   ← middle
xxxxx
xxxx
xxx
xx
x
```

Mirror symmetry.

---

## Flow Explanation

First loop grows.

Second loop shrinks.

The middle row must not repeat.

That’s why second loop starts from `n-1`.

---

## Rust Code

```rust
fn main() {
    let n = 6;

    for i in 1..=n {
        for _ in 1..=i {
            print!("x");
        }
        println!();
    }

    for i in (1..n).rev() {
        for _ in 1..=i {
            print!("x");
        }
        println!();
    }
}
```

---

# 5. Binary Triangle

## Diagram

```
1
01
101
0101
10101
```

Pattern alternates:

```
1 0 1 0 1 ...
```

---

## Flow Explanation

Each row starts with:

```
row odd → start with 1
row even → start with 0
```

Then flip every step.

Flip rule:

```
val = 1 - val
```

This toggles:

```
1 → 0
0 → 1
```

---

## Step Example (Row 4)

```
start = 0

print 0 → flip → 1
print 1 → flip → 0
print 0 → flip → 1
print 1
```

Result:

```
0101
```

---

## Rust Code

```rust
fn main() {
    for i in 1..=5 {
        let mut val = i % 2;

        for _ in 1..=i {
            print!("{}", val);
            val = 1 - val;
        }

        println!();
    }
}
```

---

# Golden Pattern Formula

Every pattern problem reduces to:

```
for each row i
    decide how many spaces
    decide how many symbols
    decide what symbol
```

That’s it.

Patterns are just math on i.

