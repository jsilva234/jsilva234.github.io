---
title: References
topic: Programming
subtopic: Rust
order: 2
---

A reference (`&T`, `&mut T`) is a pointer to a value, checked by the compiler. Compared to a C pointer:

- It is never null. Use `Option<&T>` for "maybe nothing".
- It is never dangling. The compiler proves the value outlives the reference.
- Either one `&mut T` or any number of `&T` exist at a time, never both.
- There is no pointer arithmetic.

Use `r` for the reference itself and `*r` for the value behind it. Rust adds the `*` for you in method calls, field access and printing.

```rust
let mut x = 5;
let r = &mut x;
*r += 1;                 // writing through a reference needs *
println!("{}", r);       // 6, Display follows the reference
println!("{:p}", r);     // the address stored in r
```

An explicit `*` is needed to write through `&mut`, to compare with a plain value (`*r == 5`), and to copy a value out (`let y = *r;`, only for `Copy` types).
