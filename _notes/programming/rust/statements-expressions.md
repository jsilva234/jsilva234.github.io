---
title: Statements vs Expressions
topic: Programming
subtopic: Rust
order: 2
---

An **expression** produces a value:

```rust
1 + 2          // 3
{ 1 + 2 }      // 3, a block expression
if true { 1 } else { 2 }   // 1
```

A **statement** performs an action and produces no value:

```rust
let x = 1;     // declaration, no value
```

Because `let` is a statement, it can't be used as a value:

```rust
// let a = (let b = 1);   // error: expected expression, found `let` statement
```

The `;` turns an expression into a statement, its value is discarded:

```rust
1 + 2;         // expression statement, value thrown away
```

A statement's value is `()`, the unit type:

```rust
let a = { 1 + 2; };   // a == ()
```

A block ends with an optional **tail expression** (no `;`), which becomes the block's value:

```rust
let n = {
    let a = 2;
    a * 3          // tail expression, n == 6
};
```
