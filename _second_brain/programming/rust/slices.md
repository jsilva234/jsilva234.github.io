---
title: Slices
topic: Programming
subtopic: Rust
order: 15
---

A borrowed view of contiguous elements.  
Stored as a pointer plus a length, the length is only known at runtime:

```rust
fn main() {
    let arr = [1, 2, 3, 4];
    let v = vec![1, 2, 3, 4];
    let s = String::from("abcd");

    let a = &arr[1..3];    // &[i32], from an array
    let b = &v[1..3];      // &[i32], from a Vec
    let c = &s[1..3];      // &str, from a String
    let d = &a[0..1];      // &[i32], from another slice
}
```

### Slice coercion

It's important to understand a slice is a different type from the data it references.  
E.g.: an array is `[T; N]` and a slice is `[T]`, different types:

```rust
fn main() {
    let a: [i32; 4] = [1, 2, 3, 4];    // array, length in the type
    let s: &[i32] = &a[..];            // slice, no length in the type
}
```

A reference to an array is converted to a reference to a slice by [coercion](#coercion):

```rust
fn main() {
    let arr = [1, 2, 3, 4];
    let r = &arr;                // &[i32; 4], length in the type
    let s: &[i32] = &arr;        // &[i32], length in the pointer
}
```

### Slice parameter

Because of [coercion](#coercion), a `&[T]` parameter accepts slices, but also other references you can make slices of (e.g. arrays, vectors...):

```rust
fn sum(list: &[i32]) -> i32 {
    list.iter().sum()
}

fn main() {
    let arr = [1, 2, 3, 4];
    let v = vec![1, 2, 3, 4];

    sum(&arr);           // &[i32; 4] to &[i32]
    sum(&v);             // &Vec<i32> to &[i32]
    sum(&arr[1..3]);     // already a slice
    // sum(arr);         // error: expected &[i32], found [i32; 4]
}
```
