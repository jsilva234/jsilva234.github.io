---
title: Statements vs Expressions
topic: Programming
subtopic: Rust
order: 2
---

Statements and expressions work as in C and JS:

- An **expression** is evaluated and produces a value.
- A **statement** is executed and produces no value.
- Statements

```rust
let a = 1 + 2;   // statement; 1 + 2 is an expression, a receives 3
```

### What Rust adds

Blocks (`{ }`), `if`/`else`, `match` and loops (`loop`, `while`, `for`) are expressions too.

```rust
let b = loop { break 1 };           // block, b == 1

let c = if true { 1 } else { 2 };   // if/else, c == 1

{
    let y = 1
    println!("{}", y)
} // y is no longer after this block ends
```

## Tail expression

The last expression in a block, with no `;`, is the block's value. It is called the **tail expression**:

```rust
let n = {
    let a = 2;
    a * 3 // no ";"
};
```

If it ended with `;` it would a statement that dont saves the result and the block evaluates to `unit value`

```rust
let x = { 1 + 3 };    // x == 4
let y = { 1 + 3; };   // y == ()
```