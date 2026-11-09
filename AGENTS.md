# Notes conventions

## Markdown

- When a line of prose is followed by a new line in the same paragraph, end it with a double space (two trailing spaces) so the markdown renders the line break.
- Not needed inside code blocks or before a blank line.

## Rust notes (`_notes/programming/rust/`)

- Notes are a second brain, not a tutorial: minimal and terse.
- Mostly code blocks with short `//` comments.
- Rust examples only, no C examples. The author already knows C, so only call out what differs from C/JS.
- Teach bottom-up: isolate one concept, build on it, and treat side behaviors (e.g. `println!`, auto-deref) as separate topics.
- Do not add things the author did not name (e.g. extra glossary terms).
- Ask when placement or wording is ambiguous.
