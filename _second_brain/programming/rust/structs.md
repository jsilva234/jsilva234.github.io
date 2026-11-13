---
title: Structs
topic: Programming
subtopic: Rust
order: 10
---

A struct groups named fields:

```rust
struct Rect {
    width: u32,
    height: u32,
}

let r = Rect { width: 3, height: 4 };
println!("{}", r.width);      // field access with .
```

Behavior lives in an `impl` block, separate from the data:

```rust
impl Rect {
    fn area(&self) -> u32 {   // method: first param is the instance
        self.width * self.height
    }

    fn new(width: u32, height: u32) -> Rect {   // no self: associated function
        Rect { width, height }
    }
}

let r = Rect::new(3, 4);      // associated function: Type::name
println!("{}", r.area());     // method: instance.name()
```

A type can have multiple `impl` blocks. They only need the same name as the struct, and they all add to the same type:

```rust
impl Rect {
    fn is_square(&self) -> bool { self.width == self.height }
}
```
