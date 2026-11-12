---
title: Glossary
topic: Programming
subtopic: Rust
order: 1
---

### Block expression

`{ ... }` with its own scope, evaluates to its tail expression.

```rust
let n = { let a = 2; a * 3 };
```

### Tail expression

Last expression in a block, no `;`, becomes the block's value.

```rust
a * 3
```

### Unit value

`()`, an empty tuple, Rust uses it to represent the absence of a meaningful value.

```rust
fn log() {}   // returns ()
```

### Inner scope

*(informal)* A nested block, used when the point is when its locals are dropped.

```rust
{ let y = 2; }
```

### Nested scope

*(informal)* Same as inner scope.

```rust
{ { let z = 3; } }
```

### Bare block

*(informal)* A block not attached to `if`, `fn`, `loop`, etc.

```rust
{ let y = 2; }
```

### Copy type

Assignment copies the bytes, both variables stay valid.

e.g. `i32`, `bool`, `&T`

### Reference

A pointer that borrows, no cleanup duty.

e.g. `&T`, `&mut T`

### Smart pointer

Pointer that owns and manages what it points to.

e.g. `Box<T>`, `String`, `Vec<T>`

### Lifetime

The span of code during which a reference is valid.

e.g. `'a`, `'static`

### Dangling reference

A reference to memory that has already been freed, Rust rejects it at compile time.

```rust
r = &x;   // after `x` is dropped
```
