---
type: Guide
title: "YAML Advance Concepts"
description: "Complex keys, anchors, aliases, overriding, tags, and multi-document YAML files"
generated: { by: human:bhagatabhijeet, at: 2026-09-13T04:58:00Z }
---

# YAML Advanced Concepts (for curious beginners)

Table of contents

- [Complex Keys in YAML](#complex-keys-in-yaml)
- [Anchors and Alias in YAML](#anchors-and-alias-in-yaml)
- [Overriding in YAML](#overriding-in-yaml)
- [Multiple YAML documents in a single YAML file](#multiple-yaml-documents-in-a-single-yaml-file)

## Complex Keys in YAML

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

Anchors and aliases let you identify an item with an anchor in a YAML document, and then refer back to that same item with an alias later in the same document.

- `&` is used to define an **anchor** for a chunk of values.
- `*` is used to **refer** to that chunk anywhere else in the document.
- Anchors are very useful for repetitive sections in YAML.
- Anchors and aliases sometimes remind people of pointers in C.
- The one restriction: an anchor/alias name cannot contain `[`, `]`, `,`, or `{` characters.

Let's construct a list of ExampleCorp office locations, anchor them by country, and then build a list of employees who can report to a specific country's locations.

```yaml
ExampleCorpLocations:
  USALocations: &uslocations
    - Novi, Michigan
    - Austin, Texas
    - Cary, North Carolina
    - Irving, Texas
    - San Ramon, California
    - Mountain View, California
    - San Diego, California
    - Sunrise, Florida
    - Bellevue, Washington
    - Martinez, California
    - Irvine, California
    - Portland, Oregon
  CanadaLocations: &canlocations
    - Waterloo-A
    - Waterloo-B
    - Waterloo-C
    - Mississauga
    - Ottawa
    - Vancouver
    - Halifax

employees:
  - employee:
    name: Alice
    canreportto: *uslocations
  - employee:
     name: Bob
     canreportto: *canlocations
```

Note the use of `&` and `*` to define and reuse the location lists.

The corresponding JSON:

```json
{
  "ExampleCorpLocations": {
    "USALocations": [
      "Novi, Michigan",
      "Austin, Texas",
      "Cary, North Carolina",
      "Irving, Texas",
      "San Ramon, California",
      "Mountain View, California",
      "San Diego, California",
      "Sunrise, Florida",
      "Bellevue, Washington",
      "Martinez, California",
      "Irvine, California",
      "Portland, Oregon"
    ],
    "CanadaLocations": [
      "Waterloo-A",
      "Waterloo-B",
      "Waterloo-C",
      "Mississauga",
      "Ottawa",
      "Vancouver",
      "Halifax"
    ]
  },
  "employees": [
    {
      "employee": null,
      "name": "Alice",
      "canreportto": [
        "Novi, Michigan",
        "Austin, Texas",
        "Cary, North Carolina",
        "Irving, Texas",
        "San Ramon, California",
        "Mountain View, California",
        "San Diego, California",
        "Sunrise, Florida",
        "Bellevue, Washington",
        "Martinez, California",
        "Irvine, California",
        "Portland, Oregon"
      ]
    },
    {
      "employee": {
        "name": "Bob",
        "canreportto": [
          "Waterloo-A",
          "Waterloo-B",
          "Waterloo-C",
          "Mississauga",
          "Ottawa",
          "Vancouver",
          "Halifax"
        ]
      }
    }
  ]
}
```

> Indentation pitfall: look closely at the two `employee:` entries in the YAML above. For Alice, `name` and `canreportto` are indented to the *same* level as `employee:` itself, so they end up as siblings of `employee` (which becomes `null`) rather than nested inside it. For Bob, they're indented one extra space, so they correctly nest inside `employee`. The JSON output shows exactly this difference — a good real-world reminder of why consistent indentation matters in YAML.

## Overriding in YAML

After defining an anchor, you may want to reuse the same block with some values changed. This is where **overriding** helps.

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
