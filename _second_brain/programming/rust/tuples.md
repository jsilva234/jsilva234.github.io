---
title: Tuples
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
