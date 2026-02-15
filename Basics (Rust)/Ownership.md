# Basics

> Ownership = Rust’s rule system that guarantees memory safety **without garbage collection**.

Rust forces you to answer:

👉 Who owns this memory?
👉 Who is allowed to read it?
👉 Who is allowed to change it?
👉 When is it freed?

The compiler checks all of it.

---

# 🧠 Core Mental Model

Imagine every heap value has:

👉 **exactly one owner**
👉 optional **borrowers**
👉 when owner dies → memory is freed

That’s it.

Everything else is a consequence of this.

---

# Rule 1: Every value has one owner

```rust
let s = String::from("hello");
```

`s` owns the string.

It lives on heap.

When `s` goes out of scope:

```rust
} // drop(s) runs automatically
```

Memory freed.

No `delete`, no `free`, no GC.

Rust does it automatically.

C++ equivalent:

```
RAII destructor
```

Rust just enforces it harder.

---

# Rule 2: Only one owner at a time

This is where Rust shocks C++ devs.

```rust
let s1 = String::from("hello");
let s2 = s1;
```

In C++ you'd expect a copy.

In Rust:

👉 ownership MOVES

After this:

```
s2 owns the string
s1 is invalid
```

Trying to use `s1`:

```rust
println!("{}", s1); // ❌ compile error
```

Why?

Because otherwise both would try to free the same memory → double free.

Rust prevents it at compile time.

This is called a **move**.

---

# Copy vs Move

Some types are cheap to copy:

```
integers
bool
char
float
```

These implement `Copy`.

```rust
let x = 5;
let y = x;
println!("{}", x); // OK
```

Because stack data is copied.

But heap types like `String` are moved, not copied.

---

# If you WANT a deep copy

You must say it explicitly:

```rust
let s2 = s1.clone();
```

Now both have their own heap memory.

Rust makes expensive copies visible.

No hidden performance traps.

---

# Ownership and Functions

Passing to a function = move

```rust
fn take(s: String) {}

let s = String::from("hi");
take(s);

println!("{}", s); // ❌ moved
```

Function took ownership.

`s` is dead.

Unless you return it back.

This is annoying… which leads to:

---

# Borrowing (the important part)

Borrowing = use without owning.

Like lending your book to a friend.

```rust
fn len(s: &String) -> usize {
    s.len()
}

let s = String::from("hello");
let l = len(&s);

println!("{}", s); // OK
```

We passed a reference:

```
&s
```

Function can read it.

But doesn’t own it.

So original survives.

---

# Immutable references

Default borrow = read-only

```rust
&String
```

You can have:

👉 many immutable references

```rust
let r1 = &s;
let r2 = &s;
let r3 = &s;
```

Reading is safe.

No one changes data.

---

# Mutable references

If you want to modify:

```rust
fn change(s: &mut String) {
    s.push_str("!");
}
```

Call:

```rust
let mut s = String::from("hi");
change(&mut s);
```

Now Rust enforces:

> only ONE mutable reference at a time

This is illegal:

```rust
let r1 = &mut s;
let r2 = &mut s; // ❌
```

Why?

Because 2 writers = chaos.

Rust prevents data races at compile time.

---

# The golden borrowing rule

At any moment you can have:

✅ many immutable references
OR
✅ one mutable reference

but not both

Never mix.

This rule alone eliminates:

* race conditions
* double free
* use-after-free
* dangling pointers

Entire classes of bugs vanish.

---

# Dangling references

Rust refuses this:

```rust
fn dangle() -> &String {
    let s = String::from("hi");
    &s // ❌
}
```

Because `s` dies after function ends.

Returning its reference = pointing to dead memory.

Rust says: nope.

You must return ownership:

```rust
fn ok() -> String {
    String::from("hi")
}
```

Safe.

---

# Slices (lightweight borrowing)

Slice = borrowed view into data.

No ownership.

```rust
let s = String::from("hello world");
let word = &s[0..5];
```

`word` is:

```
&str
```

It points inside `s`.

Rust ensures:

👉 you cannot modify `s` while slice exists

Because that would invalidate it.

Compile-time safety.

---

# Why all this pain exists

Because Rust promises:

✅ no garbage collector
✅ no manual memory
✅ no runtime crashes from memory
✅ zero-cost abstractions
✅ C++ performance
✅ Java-level safety

Ownership is the price.

But once it clicks, you stop fighting it.

---

# DSA intuition

When writing algorithms:

Think:

```
Who owns this data?
Do I need to modify it?
Am I just reading it?
```

Reading → `&T`
Modifying → `&mut T`
Taking ownership → `T`

Most DSA functions use references.

Rarely ownership.

---

# Ultra short cheat sheet

Ownership:

```
let b = a;   // move
let b = a.clone(); // deep copy
```

Borrow:

```
&T      // read-only
&mut T  // writable
```

Rule:

```
many readers OR one writer
```

Never both.

