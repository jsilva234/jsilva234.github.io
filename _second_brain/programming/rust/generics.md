---
title: Generics
topic: Programming
subtopic: Rust
order: 19
---

A type abstraction, replaced by concrete types at compile time.  
One copy is compiled per concrete type used, nothing generic remains at runtime:

```rust
fn id<T>(x: T) -> T {
    x
}

id(1);        // compiled as id(x: i32) -> i32
id("a");      // compiled as id(x: &str) -> &str
```

Can be declared on:

```rust
fn main() {
    fn id<T>(x: T) -> T {
        x
    }
    let a = id(1);                 // T = i32

    struct Wrapper<T> {
        v: T,
    }
    let b = Wrapper { v: "a" };    // T = &str

    enum Maybe<T> {
        Some(T),
        None,
    }
    let c = Maybe::Some(1.5);      // T = f64
    let d: Maybe<u8> = Maybe::None; // nothing to infer from, annotate

    trait Tr<T> {
        fn get(&self) -> T;
    }
    impl Tr<i32> for bool {
        fn get(&self) -> i32 {
            1
        }
    }
    let e: i32 = true.get();
}
```

### impl on a generic type

Implementing on a generic struct requires a concrete type:

```rust
fn main() {
    struct Wrapper<T> {
        v: T,
    }

    // impl Wrapper {}           // error: needs a type argument
    impl Wrapper<i32> {
        fn double(&self) -> i32 {
            self.v * 2
        }
    }

    let a = Wrapper { v: 2 };
    a.double();
}
```

To implement for any type, declare `T` right after `impl`:

```rust
fn main() {
    struct Wrapper<T> {
        v: T,
    }

    // impl Wrapper<T> {}        // error: cannot find type `T`
    impl<T> Wrapper<T> {
        fn val(&self) -> &T {
            &self.v
        }
    }

    let a = Wrapper { v: 2 };
    let b = Wrapper { v: "a" };
    a.val();
    b.val();
}
```

A generic impl needs a generic struct or trait to pass the type to:

```rust
fn main() {
    struct Point {
        x: i32,
    }
    struct Wrapper<T> {
        v: T,
    }
    trait Tr<T> {}

    // impl<T> Point {}          // error: `T` is not used by Point
    impl<T> Wrapper<T> {}        // ok: the struct takes T
    impl<T> Tr<T> for Point {}   // ok: the trait takes T
}
```

### Generic type alias

TODO

```rust
fn main() {
    type Pair<T> = (T, T);

    let a: Pair<i32> = (1, 2);
    let b: Pair<&str> = ("a", "b");
}
```
