---
title: References
topic: Programming
subtopic: Rust
order: 2
---

Rust borrow checker (compiler) validates references:
A reference (`&T`, `&mut T`) is a pointer with rules the compiler checks:

- never null (`Option<&T>` for "maybe nothing")
- never dangling
- no pointer arithmetic
- only one `&mut` is allowed, or any number of `&`, never both

```rust
let mut x = 5;

let xp = &mut x;
//let i = &x;         // COMPILER ERROR: cannot borrow `x` as immutable because it is also borrowed as mutable
*xp += 1;             // updates xp, '*' for dereference

assert!(x == 6); // pointer changes the value
assert!(*xp == 6);
```

These rules are contextual and depend on usages forward in the code. 
A usage invalidates every existing reference that is used after it, including references of references.

A shared reference used after a `&mut` is created:

```rust
let mut s = String::from("hi");

let _r1 = &s;
let _r2 = &s;             // many "&" references is fine
assert!(*_r1 == "hi");

let _m = &mut s;          // "&mut" valid unless "&" references are used.
assert!(*_r1 == "hi");    // error[E0502]: cannot borrow `s` as mutable because it is also borrowed as immutable 

```

Two `&mut` at the same time:

```rust
let mut x = 5;

let r1 = &mut x;
let r2 = &mut x;          // second &mut invalidates r1
*r1 += 1;                 // error: r1 is no longer valid, x was mutably borrowed again
```

The owner read while a reference is used later:

```rust
let mut x = 5;

let r = &mut x;
let a = x;                // reading x invalidates r
*r += 1;                  // error: r is no longer valid, x was used above
```

The owner written while a reference is used later:

```rust
let mut x = 5;

let r = &x;
x = 6;                    // writing x invalidates r
assert!(*r == 5);         // error: r is no longer valid, x was changed above
```

The owner moved while a reference is used later:

```rust
let s = String::from("hi");

let r = &s;
let t = s;                // moving s invalidates r
assert!(*r == "hi");      // error: r is no longer valid, s was moved above
```

A reference of a reference is invalidated with the first one:

```rust
let mut x = 5;

let r = &mut x;
let rr = &r;              // reference to the reference
x += 1;                   // changing x invalidates r, and rr with it
assert!(**rr == 5);       // error: rr is no longer valid, x was changed above
```

Once the last reference is used, the owner is free again:

```rust
let mut x = 5;

let r = &mut x;
*r += 1;                  // last use of r, the borrow ends here
x += 1;                   // OK
```
