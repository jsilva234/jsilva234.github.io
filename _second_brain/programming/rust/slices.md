---
title: Slices
topic: Programming
subtopic: Rust
order: 15
---

A borrowed view of contiguous elements.  
Stored as a pointer plus a length, the length is known at runtime:

```rust
fn main() {
    let arr = [1, 2, 3, 4];
    let s: &[i32] = &arr[1..3];    // address of arr[1] + len 2
    println!("{:?}", s);           // [2, 3]
}
```
