---
title: Loops
topic: Programming
subtopic: Rust
order: 10
---

`while` works typically with a `bool` condition.   
`for` works like a for each.  

### `loop`

Repeats forever until `break`.
`loop` is an expression: `break` can return a value.

```rust
let mut n = 0;
let result = loop {
    n += 1;
    if n == 3 {
        break n * 2; // the loop evaluates to 6
    }
};
```

### Named loops

A label (`'name:`) lets `break` and `continue` target an outer loop instead of the innermost one.  
Works on `loop`, `while` and `for`, and they can be mixed.

```rust
'outer: for i in 0..3 {
    let mut j = 0;
    while j < 3 {
        j += 1;
        if j == 2 {
            continue 'outer; // next `i`
        }
        if i == 2 {
            break 'outer; // exits both loops
        }
    }
}
```

Only a labeled `loop` can `break` with a value. `while` and `for` can't, they always evaluate to `()`.

```rust
let mut i = 0;
let found = 'outer: loop {
    for j in 0..3 {
        i += 1;
        if i == 5 {
            break 'outer i * 10; // `found` is 50
        }
    }
};
```
