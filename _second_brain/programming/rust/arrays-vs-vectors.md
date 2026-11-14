---
title: Arrays vs Vectors
topic: Programming
subtopic: Rust
order: 14
---

### Array

Fixed-size group of values, all the same type:

```rust
let a: [i32; 3] = [1, 2, 3];
let n = a[0];                 // access by index with []
```

### Using arrays

```rust
let mut a = [1, 2, 3];
a[0] = 5;                     // mutable with let mut
let z = [0; 5];               // repeat form: five zeros
let s = &a[1..3];             // slice: [2, 3]
// a[10] panics at runtime, bounds are checked (C would be undefined behavior)
// [i32; 3] and [i32; 4] are different types: length is part of the type
```

### Vector

Dynamic-size array: it can grow and shrink at runtime. Its values live on the heap.  
Just like arrays, all values must be of the same type:

```rust
let v: Vec<i32> = vec![1, 2, 3];
let n = v[0];                 // access by index with []
```

### Using vectors

```rust
let mut v = vec![1, 2, 3];    // macro, Vec::new() makes an empty one
v.push(4);                    // grows at runtime, length is not part of the type
let z = vec![0; 5];           // repeat form: five zeros
let s = &v[1..3];             // slice: [2, 3], same &[i32] as from an array
// v[10] panics at runtime, bounds are checked
// heap buffer managed by ptr + len + capacity
```

### Common vector methods

```rust
let mut v = vec![1, 2, 3];
v.push(4);                    // add at the end
v.pop();                      // remove the last, returns Option<i32>
v.insert(0, 9);               // insert at index, shifts the rest
v.remove(0);                  // remove at index, returns the value
v.len();                      // number of elements: 3
v.is_empty();                 // false
v.contains(&2);               // true, takes a reference
v.get(10);                    // None, no panic unlike v[10]
for x in &v {                 // iterate by reference, v is still usable after
    println!("{}", x);
}
v.clear();                    // remove all elements
```
