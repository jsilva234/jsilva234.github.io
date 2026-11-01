---
title: Ownership
topic: Programming
subtopic: Rust
order: 3
---

Three rules:

1. Each value has an owner.
2. There is only one owner at a time.
3. When the owner goes out of scope, the value is dropped.

Each value has an owner:

```rust
let s = String::from("hi");   // s owns "hi"
```

Only one owner at a time. Assigning moves ownership:

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1; // s1 is moved into s2

    // println!("{s1}"); // error: borrow of moved value
    println!("{s2}");
}
```

The value is dropped when the owner goes out of scope:

```rust
{
    let s = String::from("hi");
}                             // s goes out of scope: "hi" is dropped
```

### Copy types vs smart pointers

Assignment copies the bytes of the variable. What those bytes are decides the behavior.

A **Copy type** is its bytes, so the copy is complete and both variables stay valid:

```rust
let a = 5;                    // a's bytes: the value 5
let b = a;                    // copied, a is still valid
assert!(a == 5 && b == 5);
```

A **smart pointer** owns what it points to. Its bytes are a handle to heap data, so copying them would give two owners of one buffer. Assignment moves instead:

```rust
let s = String::from("hi");   // s's bytes: (ptr, len, cap), the "hi" lives on the heap
let t = s;                    // moved, s is dead
// s                          // error: use of moved value
```
