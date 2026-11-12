---
title: Pointers
topic: Programming
subtopic: Rust
order: 3
---

Pointers work similary to C.
* `&` for addess;
* `*` for dereference;

Rust changes:
* `&` [references](#reference) only allow reading (unmutable);
* `&mut` is required for mutable operations (only if varible is also mutable);
```
