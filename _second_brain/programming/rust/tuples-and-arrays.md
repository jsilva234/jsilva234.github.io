---
title: Tuples and Arrays
topic: Programming
subtopic: Rust
order: 13
---

### Tuple

Fixed-size group of values, types can differ:

```rust
let t: (i32, &str, f64) = (1, "hi", 2.5);
let n = t.0;                  // access by index with .
```

### Using tuples

```rust
let mut t = (1, "hi");
t.0 = 5;                      // mutable with let mut
println!("{:?}", t);          // no Display for tuples, use {:?}
let (a, b) = t;               // destructuring: a = 5, b = "hi"
let (a, _) = t;               // _ ignores a part
let s = (t.0,);               // single element needs trailing comma, (5) is just 5
let n = (t, 3);               // nesting
let x = n.0.1;                // reach into nested: "hi"
// (i32, &str) and (i32, &str, i32) are different types: length is part of the type
```

### Array

Fixed-size group of values, all the same type:

```rust
let a: [i32; 3] = [1, 2, 3];
let n = a[0];                 // access by index with []
```

### Using arrays

```rust
let mut a = [1, 2, 3];
a[0] = 5;                     // mutable with let mut
let z = [0; 5];               // repeat form: five zeros
let s = &a[1..3];             // slice: [2, 3]
// a[10] panics at runtime, bounds are checked (C would be undefined behavior)
// [i32; 3] and [i32; 4] are different types: length is part of the type
```
