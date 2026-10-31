---
title: Glossary
topic: Programming
subtopic: Rust
order: 6
---

| Term | Meaning | Example |
| --- | --- | --- |
| `Copy` type | assignment copies the bytes, both variables stay valid | `i32`, `bool`, `&T` |
| Reference | a pointer that borrows, no cleanup duty | `&T`, `&mut T` |
| Smart pointer | pointer that owns and manages what it points to | `Box<T>`, `String`, `Vec<T>` |
