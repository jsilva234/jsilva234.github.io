---
title: Static
topic: Programming
subtopic: Rust
order: 9
---

Tehre are 2 kinds of static.
`static` variables and static lifetimes (`'static`)

### `'static`

`'static` is the longest lifetime: the target lives as long as the program runs, so the reference can't dangle.  
It is the one reserved lifetime name, since `static` is a keyword.

```rust
let c: &'static str = "hi";  // a reference that is valid for the whole program
```

A string literal's bytes sit in the program, so `"hi"` is a `&'static str`.

### `const` vs `static`

```rust
const A: i32 = 5;            // inlined at each use, has no address of its own
static B: i32 = 5;           // one fixed memory location for the whole program
```

- `const`: a value the compiler pastes in wherever you use it.
- `static`: a single place in memory for the entire run, so `&B` is a `&'static i32`.

```rust
const GREETING: &str = "hi";   // type is &'static str, the lifetime is elided
```
