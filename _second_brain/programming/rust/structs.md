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

Struct update syntax builds a struct from another, overriding some fields:

```rust
let a = Rect { width: 3, height: 4 };
let b = Rect { width: 10, ..a };   // height copied from a
```

Fields that are not `Copy` are moved out of the source:

```rust
struct User {
    name: String,
    age: u32,
}

let a = User { name: String::from("Ann"), age: 30 };
let b = User { age: 31, ..a };     // name moved from a
// println!("{}", a.name);         // error: a.name was moved
println!("{}", a.age);             // ok: age is Copy, still usable
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

### Tuple struct

Fields by position, not by name:

```rust
struct Point(i32, i32);

let p = Point(1, 2);
let x = p.0;                  // access by index
```

### Unit struct

No fields, takes zero bytes:

```rust
struct Marker;

let m = Marker;               // no () and no {}
```

### Unit struct use case

A type with behavior but no data to hold:

```rust
struct Math;

impl Math {
    fn double(n: i32) -> i32 {
        n * 2
    }
}

let x = Math::double(4);      // no instance needed
```
