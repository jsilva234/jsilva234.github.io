---
title: Glossary
topic: Programming
subtopic: Rust
order: 1
---

| Term | Meaning | Example |
| --- | --- | --- |
| **Block expression** | `{ ... }` with its own scope, evaluates to its tail expression | `let n = { let a = 2; a * 3 };` |
| **Tail expression** | last expression in a block, no `;`, becomes the block's value | `a * 3` |
| **Inner scope** | *(informal)* a nested block, used when the point is when its locals are dropped | `{ let y = 2; }` |
| **Nested scope** | *(informal)* same as inner scope | `{ { let z = 3; } }` |
| **Bare block** | *(informal)* a block not attached to `if`, `fn`, `loop`, etc. | `{ let y = 2; }` |
| **Copy type** | assignment copies the bytes, both variables stay valid | `i32`, `bool`, `&T` |
| **Reference** | a pointer that borrows, no cleanup duty | `&T`, `&mut T` |
| **Smart pointer** | pointer that owns and manages what it points to | `Box<T>`, `String`, `Vec<T>` |
