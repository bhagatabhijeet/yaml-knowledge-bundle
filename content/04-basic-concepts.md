---
type: Guide
title: "YAML Basic Concepts"
description: "Scalars, sequences, mappings, comments and common pitfalls"
generated: { by: human:bhagatabhijeet, at: 2026-09-13T04:58:00Z }
---

# YAML Basic Concepts

YAML uses indentation to show structure. Keep these basic ideas in mind:

Scalars (plain values)

- Strings, numbers, booleans, and null are scalars.
- Example: `name: Alice`, `age: 30`, `is_active: true`

Sequences (lists)

```yaml
skills:
  - yaml
  - writing
  - teaching
```

Mappings (key/value pairs)

```yaml
person:
  name: Alice
  age: 30
```

Comments

- Use `#` for comments. Comments are ignored by parsers.

Multi-line strings

- Use `|` to preserve newlines, or `>` to fold newlines into spaces.

```yaml
bio: |
  Line one
  Line two
folded: >
  This is a long sentence
  that will be folded into
  a single line.
```

Flow style (inline)

- YAML supports inline mapping and sequence like JSON:

```yaml
inline_map: {a: 1, b: 2}
inline_list: [one, two, three]
```

Common pitfalls

- Mixing tabs and spaces — always use spaces.
- Wrong indentation levels — rely on your editor's indentation helpers.

Exercise

Write a YAML snippet for a simple todo item with a title, due date, and a list of tags.

Example answer:

```yaml
todo:
  title: "Buy groceries"
  due: 2026-09-20
  tags:
    - shopping
    - errands
```
