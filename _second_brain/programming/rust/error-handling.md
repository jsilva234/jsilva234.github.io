---
title: TODO Error Handling
topic: Programming
subtopic: Rust
order: 16
---

### `Option`

Rust has no null. `Option<T>` is a std enum for a value that may be absent:

```rust
enum Option<T> {
    Some(T),
    None,
}

let a: Option<i32> = Some(5);
let b: Option<i32> = None;
```

### `Result`

A std enum for an operation that may fail:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}

let a: Result<i32, String> = Ok(5);
let b: Result<i32, String> = Err(String::from("failed"));
```
