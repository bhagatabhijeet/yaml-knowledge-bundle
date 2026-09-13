---
type: Guide
title: "YAML Advance Concepts"
description: "Complex keys, anchors, aliases, overriding, tags, and multi-document YAML files"
generated: { by: human:bhagatabhijeet, at: 2026-09-13T04:58:00Z }
---

# YAML Advanced Concepts (for curious beginners)

These are the features you'll bump into once you start *reading* other people's YAML — a Kubernetes manifest, a CI pipeline, a shared config file — rather than things you need to memorize to write your own. Skim through once so none of it looks alien later; you can always come back and copy an example when you actually need it.

Table of contents

- [Complex Keys in YAML](#complex-keys-in-yaml)
- [Anchors and Alias in YAML](#anchors-and-alias-in-yaml)
- [Overriding in YAML](#overriding-in-yaml)
- [Multiple YAML documents in a single YAML file](#multiple-yaml-documents-in-a-single-yaml-file)

## Complex Keys in YAML

Fair warning up front: complex keys are rare in real-world YAML. Almost everything you write will use a plain word as a key (like `name:` or `age:`). This section exists so the `?` syntax doesn't confuse you if you ever spot it — not because you'll need to write it often.

A complex key is a key that is itself a multiline string, a sequence, or another non-scalar structure — not just a plain word. Complex keys begin with a `?` (question mark).

```yaml
# Complex key example 1 - multiline string as a key
? this is an
  example of
  a complex key
: this is its value

# Complex key example 2 - sequence as a key
? - x
  - y
  - z
: [1, 2, 3]

# Complex key example 3 - sequence as a key, a more practical example
? - dev
  - qa
  - production
: - https://dev.server.com
  - https://qa.server.com
  - https://prod.server.com
```

## Anchors and Alias in YAML

![Anchors and aliases](assets/images/yaml-anchors.svg)

Think of an anchor as giving a **nickname** to a block of YAML, so you can reuse it later by name instead of retyping (or copy-pasting) the whole thing.

- `&` is used to define an **anchor** for a chunk of values — like saying "call this block `uslocations`."
- `*` is used to **refer** to that chunk anywhere else in the document — "insert `uslocations` here."
- Anchors are very useful for repetitive sections in YAML.
- Anchors and aliases sometimes remind people of pointers in C.
- The one restriction: an anchor/alias name cannot contain `[`, `]`, `,`, or `{` characters.

Let's construct a small list of ExampleCorp office locations, anchor them by country, and then say which employee can report to which country's locations.

```yaml
ExampleCorpLocations:
  USALocations: &uslocations
    - San Ramon, California
    - Austin, Texas
    - Portland, Oregon
  CanadaLocations: &canlocations
    - Waterloo
    - Ottawa
    - Vancouver

employees:
  - employee:
    name: Alice
    canreportto: *uslocations
  - employee:
     name: Bob
     canreportto: *canlocations
```

Note the use of `&` and `*` to define and reuse the location lists — `*uslocations` simply expands to the same three-item list defined above.

The corresponding JSON:

```json
{
  "ExampleCorpLocations": {
    "USALocations": ["San Ramon, California", "Austin, Texas", "Portland, Oregon"],
    "CanadaLocations": ["Waterloo", "Ottawa", "Vancouver"]
  },
  "employees": [
    {
      "employee": null,
      "name": "Alice",
      "canreportto": ["San Ramon, California", "Austin, Texas", "Portland, Oregon"]
    },
    {
      "employee": {
        "name": "Bob",
        "canreportto": ["Waterloo", "Ottawa", "Vancouver"]
      }
    }
  ]
}
```

> Indentation pitfall: look closely at the two `employee:` entries in the YAML above. For Alice, `name` and `canreportto` are indented to the *same* level as `employee:` itself, so they end up as siblings of `employee` (which becomes `null`) rather than nested inside it. For Bob, they're indented one extra space, so they correctly nest inside `employee`. The JSON output shows exactly this difference — a good real-world reminder of why consistent indentation matters in YAML.

## Overriding in YAML

After defining an anchor, you may want to reuse the same block but change just one or two values. This is like inheriting someone else's settings and tweaking only the field you care about — that's what **overriding** does.

- To override, use `<<:` before the alias.
- This merges the anchored mapping into the current mapping, and any keys you redefine below take precedence.

In the following example, `qa`, `dev`, and `prod` environments are defined once and anchored. In `deployTo`, the anchored environments are merged in, but the `qa` value is overridden.

```yaml
---
environments:
  defined_environments: &definedenv
    qa: https://qa
    dev: https://dev
    prod: https://prod

deployTo:
  <<: *definedenv
  qa: https://newqa
```

Note the use of `<<:` before the alias `*definedenv` to merge in the anchored mapping.

The corresponding JSON:

```json
{
  "environments": {
    "defined_environments": {
      "qa": "https://qa",
      "dev": "https://dev",
      "prod": "https://prod"
    }
  },
  "deployTo": {
    "qa": "https://newqa",
    "dev": "https://dev",
    "prod": "https://prod"
  }
}
```

## Multiple YAML documents in a single YAML file

This is rare in application config files, but common in tools like Kubernetes, where one file can describe several resources back to back, each separated by `---`.

- A document starts with three dashes (`---`) and ends with three dots (`...`).
- Some YAML processors require the document start marker — for example, Java's Jackson will not process a YAML document without `---`, while Python's PyYAML will.
- The end marker (`...`) is usually optional.
- When converting to JSON, only the first YAML document in the file will be parsed, because JSON has no concept of multiple documents in a single file.

```yaml
---
doc: first
---
doc: second
...
```

## Tags and explicit types

- YAML can tag nodes with explicit types (see [YAML Basic Concepts](04-basic-concepts.md#implicit-and-explicit-typing-in-yaml)) — use this sparingly in simple configs.
- Example: `!!str "123"` forces the value to be treated as a string rather than a number.

## Exercise

Use an anchor to avoid repeating the same database connection settings for two services.

Hint (short): define `db: &db` and reference `*db` in both service definitions.
