---
title: Static
topic: Programming
subtopic: Rust
order: 9
---

TODO: review and trim this note.

A reference is only valid while its target exists:

```rust
let r;
{
    let x = 5;
    r = &x;
}                      // x is dropped here
// println!("{}", r);  // error: `x` does not live long enough
```

A literal's bytes aren't owned by any block, so the reference stays valid:

```rust
let r;
{
    r = "hello";       // bytes live in the program, not in this block
}
println!("{}", r);     // ok
```

`'static` is a lifetime: the target lives as long as the program runs, so the reference can't dangle.

### `const` vs `static` vs `'static`

```rust
const A: i32 = 5;            // inlined at each use, has no address of its own
static B: i32 = 5;           // one fixed memory location for the whole program
let c: &'static str = "hi";  // a reference that is valid for the whole program
```

- `const`: a value the compiler pastes in wherever you use it.
- `static`: a single place in memory for the entire run, so `&B` is a `&'static i32`.
- `'static`: the lifetime on the reference. A string literal's bytes sit in the program like a `static`, so `"hi"` is a `&'static str`.

```rust
const GREETING: &str = "hi";   // type is &'static str, the const holds a reference
```
