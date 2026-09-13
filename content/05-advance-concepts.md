---
title: "YAML Advance Concepts"
---

# YAML Advanced Concepts (for curious beginners)

Anchors and aliases

- Anchors let you define a value once and reuse it elsewhere using aliases.

```yaml
defaults: &defaults
  timeout: 30
  retries: 3

serviceA:
  <<: *defaults
  endpoint: /service-a

serviceB:
  <<: *defaults
  endpoint: /service-b
```

- `&defaults` creates an anchor. `*defaults` refers to it. `<<:` is used to merge mappings.

Tags and types

- YAML can tag nodes with types (use rarely in simple configs).
- Example: `!!str "123"` forces the value to be a string.

Complex multi-line formats

- You can embed YAML lists or maps inside multi-line strings if needed.

Flow style vs block style

- Block style (indentation) is most readable. Flow style is compact but harder to read by hand.

Exercise

Use an anchor to avoid repeating the same database connection settings for two services.

Hint (short): define `db: &db` and reference `*db` in both service definitions.
