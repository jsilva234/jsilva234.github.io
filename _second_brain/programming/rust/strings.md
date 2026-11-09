---
title: Strings
topic: Programming
subtopic: Rust
order: 8
---

A Rust string is bytes guaranteed to be valid UTF-8.

```rust
let s = "hé";           // 'h' = 1 byte, 'é' = 2 bytes
s.len();                // 3, bytes, not chars
s.chars().count();      // 2
// s[1]                 // error: no indexing, a byte index could land mid-char
```

### `str` type

`str` is the text itself, as raw bytes in memory: no pointer, no length.  
When you write `"hi"` in your code, the characters `hi` get stored inside the program.   
Those stored characters are the `str`:

```rust
let size: usize = "str".len(); //"str" is a string 
// literal, it exists because it's declared on the code,  
```

To use a `str` around you need a pointer to it:
```rust
let s: &str = "hi"; // s points to the location of the `str` literal "hi"            
```

So in practice `str` is only used as a "literal" or as a type.  

```rust
let b: Box<str> = "hi".into(); // str is the type behind the 
//Box pointer, which owns the bytes on the heap
```


### `String` vs `&str`
`&str` is a `str` pointer. It stores `ptr` + `len`. Its size is fixed.  
`String` manages a buffer on the heap and provides an API of allowed behaviors.    

```rust
let lit: &str = "hello";                   // borrowed view: ptr + len
let owned: String = String::from("hello"); // owner: ptr + len + capacity, bytes on the heap
```

In practice, `&str` is used to read a `String`. To edit text you need the `String` itself.  
This is relevant on function signatures and return types.  

```rust
fn read(s: &str) { println!("{}", s); }

let owned = String::from("hello");
read(&owned);    // &String is accepted as &str
read("hello");   // a literal is already a &str
```

A `&String` can be used wherever a `&str` is expected, but not the other way around.
With `fn read(s: &String)`, `read("hello")` would not compile: a literal is a `&str`, not a `&String`.


Because `&str` stores the `len`, it can point to a slice of a `String`.

### Type of a literal

```rust
let s: &str = "hé";             // elided form
// TODO: 'static, the literal's bytes live in the binary's read-only data and are never freed
let s: &'static str = "hé";     // full form
```
