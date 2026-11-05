---
title: References
topic: Programming
subtopic: Rust
order: 3
---

A reference (`&T`, `&mut T`) is a pointer with rules the compiler checks:

- never null (`Option<&T>` for "maybe nothing")
- never dangling
- no pointer arithmetic

```rust
let mut x = 5;

let xp = &mut x;
*xp += 1;             // updates xp, '*' for dereference

assert!(*xp == 6);
assert!(x == 6);      // pointer changes the value
```
