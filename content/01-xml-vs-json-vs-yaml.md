---
title: "XML vs JSON vs YAML"
---

# XML vs JSON vs YAML

Short comparison

- XML
  - Verbose, uses tags (good for documents and strict schemas)
  - Well supported in older systems
- JSON
  - Compact, machine-friendly, native to JavaScript
  - Good for APIs and data interchange
- YAML
  - Human-friendly, readable, supports comments and complex features
  - Great for configuration and long-hand examples

When to use

- Use YAML for configuration files and examples where humans edit the file.
- Use JSON for web APIs and where strict machine parsing is primary.
- Use XML for document-style data or legacy systems requiring schema validation.

Tiny examples (equivalent content)

JSON:

```json
{
  "person": {"name": "Alice", "age": 30, "skills": ["yaml", "writing"]}
}
```

YAML equivalent:

```yaml
person:
  name: Alice
  age: 30
  skills:
    - yaml
    - writing
```

XML equivalent:

```xml
<person>
  <name>Alice</name>
  <age>30</age>
  <skills>
    <skill>yaml</skill>
    <skill>writing</skill>
  </skills>
</person>
```

Short notes for beginners

- YAML is easier to read and write by hand because it drops closing tags and uses indentation.
- JSON is stricter (no comments) which makes it better for API payloads but worse for hand editing.

Exercise

Convert this JSON to YAML:

```json
{"colors": ["red", "green", "blue"], "primary": "red"}
```

Answer (hint: use a mapping and a sequence):

```yaml
colors:
  - red
  - green
  - blue
primary: red
```
