---
title: Flow control
topic: Programming
subtopic: Rust
order: 18
---

### `if` / `else if` / `else`

No parentheses around the condition. Braces are mandatory.  
The condition must be a `bool`: no truthy/falsy values.

```rust
let n = 5;

if n < 0 {
    println!("negative");
} else if n == 0 {
    println!("zero");
} else {
    println!("positive"); // positive
}

if n { }      // error: expected `bool`, found integer
```

### Ternary operator

Rust has no ternary operator.  
Given that `if` is an [expression](statements-vs-expressions.md#what-rust-adds), it can be used as such.  
It works as a ternary as long as both blocks end in a tail expression that evaluates to the expected type.  
The blocks can hold more code before the tail expression.

```rust
let n = 5;
let sign = if n < 0 { "negative" } else { "positive" }; // "positive"
```

### `match`

Runs the arm of the first pattern that matches the value.  
Must cover every possible value. `_` matches anything.  
An `if` after the pattern (a guard) adds an extra condition to the arm.

```rust
let n = 3;
let strict = true;

match n {
    // `if strict` is a match guard: the arm only runs if it is true
    3 if strict => println!("strict three"),
    3 => println!("three"),
    _ => println!("other"),
}
```

### `if let`

Runs the block only if the value matches the pattern.  
`if let` always compares the value against a pattern, the "template", written between `let` and `=`.  
It also creates the names in the pattern when it matches.

```rust
let a: Result<i32, String> = Ok(2);
if let Ok(n) = a {                      // expects Ok(2), n binds to 2
    println!("{}", n);                  // 2
}

let p = (0, 7);
if let (0, y) = p {                     // first must be 0, y binds the second
    println!("on the axis, y = {}", y); // on the axis, y = 7
}
```

### `let else`

If the pattern matches, bind its names. Otherwise run the `else` block.  
e.g. if `s.parse::<i32>()` is `Ok`, bind its value to `n` and continue. Otherwise `else` runs.  
The `else` block must not fall through: it ends with `return`, `panic!`, `break`, etc.

Useful to validate [Result](error-handling.md#result-usage) and [Option](null-none-results.md#option-use) outputs

```rust
let s = "2";
let Ok(n) = s.parse::<i32>() else {
    panic!("can't parse: {s}");
};
println!("{}", n);                  // 2

let p = (0, 7);
let (0, y) = p else {
    panic!("first isn't 0");
};
println!("on the axis, y = {}", y); // on the axis, y = 7
```
