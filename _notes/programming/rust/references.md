---
title: References
topic: Programming
subtopic: Rust
order: 2
---

A reference (`&T`, `&mut T`) is a pointer with rules the compiler checks:

- never null (`Option<&T>` for "maybe nothing")
- never dangling
- no pointer arithmetic
- one `&mut`, or any number of `&`, never both

Same two operations as a pointer, but following it is safe.

```rust
let mut x = 5;

let r = &mut x;      // take the address
*r += 1;             // follow it, write
let y = *r;          // follow it, read (Copy types only)

assert!(x == 6 && y == 6);
```

Same address check:

```rust
let a = 5;
let r1 = &a;
let r2 = &a;

assert!(std::ptr::eq(r1, r2));   // same address
assert!(r1 == r2);               // compares the values behind, not the addresses
```

The rules in action:

```rust
let mut s = String::from("hi");

let r1 = &s;
let r2 = &s;             // many & is fine
// let m = &mut s;       // error: r1, r2 still alive
assert!(r1.len() == r2.len());
```
