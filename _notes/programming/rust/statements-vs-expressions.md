---
title: Statements vs Expressions
topic: Programming
subtopic: Rust
order: 2
---

Statements and expressions work as in C and JS:

- An **expression** is evaluated and produces a value.
- A **statement** is executed and produces no value.
- A `;` ends a statement.

```rust
let a = 1 + 2;   // statement; 1 + 2 is an expression, a receives 3
```

### What Rust adds

Blocks (`{ }`), `if`/`else`, `match` and loops (`loop`, `while`, `for`) are expressions too.

```rust
let b = loop { break 1 };           // loop, b == 1

let c = if true { 1 } else { 2 };   // if/else, c == 1

{
    let y = 1;
    println!("{}", y)
} // doesn't end with ';'
```

#### Tail expression

The last expression in a block, with no `;`, is the block's value. It is called the **tail expression**:

```rust
let n = {
    let a = 2;
    a * 3 // no ";"
};
```

With a `;` the last line becomes a statement, so the block has no tail expression and evaluates to `()`, the unit value:

```rust
let x = { 1 + 3 };    // x == 4
let y = { 1 + 3; };   // y == ()
```