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

### Unrecoverable error

```rust
panic!("something broke"); // thread 'main' panicked at src/main.rs:2:5: something broke
```

### Null/None results 

Rust has no `null` or `None` concept. Instead, the rust way is to use the `Option<T>` enum.  
This provides a standardized interface to either return a value or a representation of "no value" (`None`)  
The Enum has 2 variants: `Some(T)` or `None`  
`Option`, `Some` and `None` are part of the [prelude](#prelude). Can be used without import.

```rust
let a: Option<i32> = Some(5);
let b: Option<i32> = None;
```

e.g. A lookup that may find nothing returns `None` instead of panicking:

```rust
let v = vec![1, 2, 3];
let a = v.get(1);             // Some(&2)
let b = v.get(10);            // None
```

### `Option` use

A function that may have nothing to return declares it in its return type:

```rust
fn first_even(v: &[i32]) -> Option<i32> {
    for &n in v {
        if n % 2 == 0 {
            return Some(n);
        }
    }
    None
}

let a = first_even(&[1, 2, 4]); // Some(2)
let b = first_even(&[1, 3]);    // None
```

### Interaction with `?` operator (`Option`)

On `Some(v)` it gives `v`. On `None` it returns `None` from the enclosing function.  
Only works in a function that returns an `Option`.

```rust
fn double_first_even(v: &[i32]) -> Option<i32> {
    let n = first_even(v)?;
    Some(n * 2)
}

let a = double_first_even(&[1, 2, 4]); // Some(4)
let b = double_first_even(&[1, 3]);    // None
```

### `unwrap` (`Option`)

On `Some(v)` it gives `v`. On `None` it panics.

```rust
let a = first_even(&[1, 2, 4]).unwrap(); // 2
let b = first_even(&[1, 3]).unwrap();    // panics: called `Option::unwrap()` on a `None` value
```
