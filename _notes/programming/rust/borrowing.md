---
title: Borrowing
topic: Programming
subtopic: Rust
order: 4
---

A reference lets you use a value without taking ownership of it. Creating one is called borrowing. The borrow checker (the compiler) validates every borrow.

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

A borrow lasts from where the reference is created to its last use, not to the end of the scope. These rules are contextual and depend on usages forward in the code. A usage invalidates every existing reference that is used after it, including references of references.

NOTE: the compiler reports these errors on the owner (`x` is "borrowed"), not on the reference.

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

Reading borrow checker errors: the message is about the owner, described as borrowed. The reference only appears in the labels below it.

```
error: cannot use `x` because it was mutably borrowed
error: cannot assign to `x` because it is borrowed
error: cannot move out of `s` because it is borrowed
```

```
let r = &mut x;   <- borrow of `x` occurs here
*r += 1;          <- borrow later used here
```
