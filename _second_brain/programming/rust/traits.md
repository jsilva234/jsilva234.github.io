---
title: Traits
topic: Programming
subtopic: Rust
order: 12
---

### Trait

A set of method signatures a type can promise to have:

```rust
trait Speak {
    fn speak(&self) -> String;    // signature only, no body
}
```

### Implementing a trait

`impl Trait for Type` provides the bodies, so one function can work with any type that implements the trait:

```rust
struct Dog;

impl Speak for Dog {
    fn speak(&self) -> String {
        String::from("woof")
    }
}

fn announce(x: &impl Speak) {   // any type that implements Speak
    println!("{}", x.speak());
}

fn main() {
    announce(&Dog);
}
```
