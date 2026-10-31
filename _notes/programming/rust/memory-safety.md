---
title: unsafe
topic: Programming
subtopic: Rust
order: 5
---

By default all code in Rust is safe. This means the compiler will not allow a variable reference to outlive a variable owner.

```rust
let r;
{
    let x = 5;
    r = &x;
}                 // x is freed with the end of this scope
*r                // compiler will not allow this. x did not live long enough
```

`unsafe` unlocks a short list of operations, mainly dereferencing a raw pointer.
The developer can take responsibility and the compiler will not complain about this action.

```rust
let s = String::from("hi");
let p = s.as_ptr();  // raw pointer to the heap bytes "hi"
let c = s;           // ownership moves to c, the heap data is still alive

// let d = *p;       // error: dereference of raw pointer is unsafe

unsafe { // unsafe only unlocks *p, validity is on the developer
    let d = *p;      // reads the first byte, b'h'
    println!("{}", d);
}
```
