---
title: Pointers
topic: Programming
subtopic: Rust
order: 1
---

A pointer is a value that holds a memory address. Rust has raw pointers (`*const T`, `*mut T`), which behave like C pointers and need `unsafe` to dereference, and references, which are the safe kind used almost everywhere.

`{:p}` prints the address a pointer holds. It uses the `Pointer` trait, which `i32` and other plain values don't implement.

```rust
let x = 5;
let r = &x;
println!("x lives at {:p}", &x);
println!("r holds     {:p}", r);   // same address as x
println!("r lives at {:p}", &r);   // r has its own address
```

```
 stack
┌─────────────────────┐
│ x: 5                │  0x7ffc...a4
├─────────────────────┤
│ r: 0x7ffc...a4  ────┼──► points to x
└─────────────────────┘  0x7ffc...a8
```
