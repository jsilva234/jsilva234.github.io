---
title: Borrowing
topic: Programming
subtopic: Rust
order: 4
---

A reference lets you use a value without taking ownership of it. Creating one is called borrowing.

```rust
fn len(s: &String) -> usize {
    s.len()
}

fn main() {
    let s = String::from("hello");
    let n = len(&s); // s is borrowed, not moved
    println!("{s} has {n} bytes");
}
```

A mutable reference allows changing the borrowed value.

```rust
fn shout(s: &mut String) {
    s.push('!');
}

fn main() {
    let mut s = String::from("hello");
    shout(&mut s);
    println!("{s}");
}
```

At any given time, you can have either one mutable reference or any number of shared references, never both. References must always be valid, so Rust rejects dangling ones at compile time.

```rust
fn main() {
    let mut s = String::from("hello");
    let r1 = &s;
    let r2 = &s; // fine: many shared references
    // let r3 = &mut s; // error: cannot borrow as mutable while borrowed
    println!("{r1} {r2}");
}
```
