---
title: Error Handling
topic: Programming
subtopic: Rust
order: 17
---

Rust has no exceptions. Instead, the rust way is to use the `Result<T, E>` enum.  
This provides a standardized interface to either return a result or an error  
The Enum has 2 variants: `Ok(T)` or `Err(E)`  
`Result`, `Ok` and `Err` are part of the [prelude](#prelude). Can be used without import.

```rust
let a: Result<i32, String> = Ok(5);
let b: Result<i32, String> = Err(String::from("failed"));
```

e.g. An operation that may fail returns `Err` with the reason:

```rust
let a = "5".parse::<i32>();   // Ok(5)
let b = "abc".parse::<i32>(); // Err(ParseIntError)
```

### `Result` usage

A function that can fail declares it in its return type:

```rust
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        return Err(String::from("division by zero"));
    }
    Ok(a / b)
}

let a = divide(6, 3);         // Ok(2)
let b = divide(6, 0);         // Err("division by zero")
```

### Interaction with `?` operator

Rust has syntax sugar to deal with a `Result`: the `?` operator.  
It stands after an expression that returns a `Result`.  
On `Ok(v)` it gives `v`. On `Err(e)` it returns `Err(e)` from the enclosing function.  
Only works in a function that returns a `Result`.

```rust
fn half_of_division(a: i32, b: i32) -> Result<i32, String> {
    let n = divide(a, b)?;
    Ok(n / 2)
}

let a = half_of_division(8, 2); // Ok(2)
let b = half_of_division(8, 0); // Err("division by zero")
```

### `unwrap`

On `Ok(v)` it gives `v`. On `Err` it panics.

```rust
let a = divide(6, 3).unwrap(); // 2
let b = divide(6, 0).unwrap(); // panics: called `Result::unwrap()` on an `Err` value: "division by zero"
```

Check [`let else`](conditional-structures.md#let-else) for validation of output.

### Unrecoverable error

```rust
panic!("something broke"); // thread 'main' panicked at src/main.rs:2:5: something broke
```
