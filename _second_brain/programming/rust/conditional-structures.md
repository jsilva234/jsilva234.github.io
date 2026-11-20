---
title: TODO Conditional Structures
topic: Programming
subtopic: Rust
order: 18
---

- `if` / `else if` / `else`
- `if` as an expression
- `match`
- `match` guards
- `if let`
- `let else`
- `while let`
- `matches!`

### `if let`

Runs the block only if the value matches the pattern. The pattern's names are bound inside the block.

```rust
let a: Result<i32, String> = Ok(2);

if let Ok(n) = a {
    println!("{}", n); // 2
}
```
