---
title: Null/None Results
topic: Programming
subtopic: Rust
order: 20
---

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
