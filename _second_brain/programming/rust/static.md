---
title: Static
topic: Programming
subtopic: Rust
order: 9
---

There are 2 kinds of static.  
`static` variables and static [lifetimes](#lifetime) (`'static`)

### static variables

A single place in memory for the entire run. It is Rust's global variable.  
Can be declared outside a function.  

```rust
static B: i32 = 5;   // needs an explicit type and a value computable at compile time

fn main() {
    println!("{}", B)
}
```
A `static` can be `mut`, but every access is `unsafe`:

```rust
static mut COUNT: i32 = 0;

unsafe { COUNT += 1; }
```

A `static` variable keeps its value between calls:

```rust
fn count_calls() -> (i32, i32) {
    static mut CALLS: i32 = 0;   // initialized once, not on every call
    let mut local = 0;           // a new variable on every call
    local += 1;
    unsafe {
        CALLS += 1;
        (CALLS, local)
    }
}

count_calls();   // (1, 1)
count_calls();   // (2, 1), CALLS kept its value, local started over
count_calls();   // (3, 1)
```

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
println!("{}", r);        // error: `x` does not live long enough
```

A `&'static` reference never dangles, so the same shape compiles:

```rust
let r;
{
    let s: &'static str = "hello";   // a local holding a reference
    r = s;                           // copies the reference, the bytes live in the program
}
println!("{}", r);                 // ok
```

A reference to a `static` variable is a `&'static`, since the variable lives for the whole run:

```rust
static B: i32 = 5;
let r: &'static i32 = &B;
```
```rust
fn f() -> &'static i32 {
    static A: i32 = 5;   // the same variable on every call of f
    &A                   // a reference to it is valid anywhere, so it can be returned
}
```

The reverse isn't needed: a `&'static` doesn't have to point at a `static` variable, a string literal is one too.

### `const` vs `static`
- `const`: works like a placeholder, the compiler just replaces each use with its value. There is no variable at runtime.  
- `static`: a variable with one fixed address for the entire run.

```rust
const A: i32 = 5;            // placeholder, each use is replaced by 5
static B: i32 = 5;           // one fixed memory location for the whole program
```

