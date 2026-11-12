---
title: Static
topic: Programming
subtopic: Rust
order: 9
---

There are 2 kinds of static.  
`static` variables and static [lifetimes](#lifetime) (`'static`)

### `'static`

`'static` is the longest [lifetime](#lifetime): the target lives as long as the program runs, so the [reference](#reference) can't [dangle](#dangling-reference).  
It is the one reserved [lifetime](#lifetime) name, since `static` is a keyword.

To understand check the following example where a reference to a local is [dangling](#dangling-reference) once its block ends, so the compiler rejects it:

```rust
let r;
{
    let x = 5;
    r = &x;                // x is dropped at the end of this block
}
println!("{}", r);      // error: `x` does not live long enough
```

A `&'static` reference never dangles, so the same shape compiles:

```rust
let r;
{
    let s: &'static str = "hello";   // a local holding a reference
    r = s;                           // copies the reference, the bytes live in the program
}
println!("{}", r);         // ok
```

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
