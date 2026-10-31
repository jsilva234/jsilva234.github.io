---
title: Pointers
topic: Programming
subtopic: Rust
order: 1
---

A pointer is a variable whose value is a memory address. Two operations: take an address (`&`), follow an address (`*`).

```rust
let mut x = 5;

let r = &mut x;      // take the address of x, r holds it
*r = 6;              // follow the address, write
let y = *r;          // follow the address, read

assert!(x == 6 && y == 6);
```
