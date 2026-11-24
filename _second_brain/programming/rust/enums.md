---
title: Enums
topic: Programming
subtopic: Rust
order: 18
---

### Enum

A type that is exactly one of its variants:

```rust
enum Direction {
    Up,
    Down,
}

let d = Direction::Up;        // variants are namespaced: Type::Variant
```

### Variants with data

Each variant can carry its own data:

```rust
struct Point {
    x: f64,
    y: f64,
}

enum Shape {
    Circle(f64),                        // tuple variant, one value
    Rect(f64, f64),                     // tuple variant, several values
    Square { side: f64 },               // struct-like variant
    Dot(Point),                         // existing struct
}

let a = Shape::Circle(1.5);
let b = Shape::Rect(3.0, 4.0);
let c = Shape::Square { side: 2.0 };
let d = Shape::Dot(Point { x: 1.0, y: 2.0 });
```

### Discriminant

The integer tied to a variant. `as` casts the enum to it:

```rust
enum Status {
    Ok = 200,
    NotFound = 404,
}

println!("{}", Status::NotFound as i32);   // 404
```

Must be an integer, `isize` by default. `#[repr]` picks another integer type:

```rust
#[repr(u8)]
enum Byte {
    A = 1,
    B = 255,      // must fit in u8
}
```

### `impl` on an enum

Methods work the same as on a struct:

```rust
enum Direction {
    Up,
    Down,
}

impl Direction {
    fn is_up(&self) -> bool {
        matches!(self, Direction::Up)
    }
}

println!("{}", Direction::Up.is_up());
```
