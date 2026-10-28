---
title: Ownership
topic: Programming
subtopic: Rust
---

Each value in Rust has a single owner. When the owner goes out of scope, the value is dropped.

```rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1; // s1 is moved into s2

    // println!("{s1}"); // error: borrow of moved value
    println!("{s2}");
}
```
