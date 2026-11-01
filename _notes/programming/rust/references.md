---
title: References
topic: Programming
subtopic: Rust
order: 2
---

Rust borrow checker (compiler) validates references:
A reference (`&T`, `&mut T`) is a pointer with rules the compiler checks:

- never null (`Option<&T>` for "maybe nothing")
- never dangling
- no pointer arithmetic
- only one `&mut` is allowed, or any number of `&`, never both

```rust
let mut x = 5;

let r = &mut x;      // take the address
let y = *r;          // follow it, read (Copy types only)
*r += 1;             // updates r, leaves y alone

assert!(x == 6 && y == 5);
```

Same address check:

```rust
let a = 5;
let r1 = &a;
let r2 = &a;

assert!(std::ptr::eq(r1, r2));   // same address
```

The rules in action:

```rust
let mut s = String::from("hi");

let r1 = &s;
let r2 = &s;             // many & is fine
// let m = &mut s;       // error: r1, r2 still alive
assert!(r1.len() == r2.len());
```
