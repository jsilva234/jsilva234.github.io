---
title: Collections
topic: Programming
subtopic: Rust
order: 21
---

### HashMap

Key-value pairs, looked up by key. Unordered.  
Equivalent to Python's `dict`.  
Most common use: lookup by key.

```rust
use std::collections::HashMap;

let mut m = HashMap::new();
m.insert("a", 1);
let v = m.get("a");           // Some(&1)
```

### HashSet

Unique values, unordered.  
Equivalent to Python's `set`.  
Most common use: membership test and removing duplicates.

```rust
use std::collections::HashSet;

let mut s = HashSet::new();
s.insert(1);
s.insert(1);                  // duplicate, ignored
let has = s.contains(&1);     // true
```

### VecDeque

Double-ended queue: fast push and pop at both ends.  
Most common use: a FIFO queue.

```rust
use std::collections::VecDeque;

let mut q = VecDeque::new();
q.push_back(1);               // enqueue at the back
q.push_back(2);
let first = q.pop_front();    // dequeue from the front: Some(1)
```

### LinkedList

Doubly linked list. Rarely the right choice, `Vec` or `VecDeque` are usually faster.  
Most common use: cheap splitting and appending of whole lists.

```rust
use std::collections::LinkedList;

let mut l = LinkedList::new();
l.push_back(1);
l.push_front(0);              // [0, 1]
```

### BTreeMap

Key-value pairs kept sorted by key.  
Most common use: iterating in key order or querying ranges.

```rust
use std::collections::BTreeMap;

let mut m = BTreeMap::new();
m.insert(2, "b");
m.insert(1, "a");
for (k, v) in &m {            // iterates in key order: 1, then 2
    println!("{} {}", k, v);
}
```

### BTreeSet

Unique values kept sorted.  
Most common use: unique values iterated in order.

```rust
use std::collections::BTreeSet;

let mut s = BTreeSet::new();
s.insert(2);
s.insert(1);
for x in &s {                 // iterates sorted: 1, then 2
    println!("{}", x);
}
```

### BinaryHeap

Priority queue: always pops the largest value first.  
Most common use: repeatedly getting the max.

```rust
use std::collections::BinaryHeap;

let mut h = BinaryHeap::new();
h.push(1);
h.push(5);
let top = h.pop();            // Some(5)
```
