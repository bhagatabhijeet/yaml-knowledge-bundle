---
type: Guide
title: "Validating YAML using yamllint"
description: "Install and use yamllint to catch common YAML issues"
generated: { by: human:bhagatabhijeet, at: 2026-09-13T04:58:00Z }
---

# Validating YAML using yamllint

![Write, lint, fix, ship](../assets/images/yaml-lint-flow.svg)

Why validate?

- Small mistakes (tabs, trailing spaces, bad indentation) can break YAML parsers.
- `yamllint` helps catch style and syntax issues early.

Install `yamllint`

`yamllint` is a Python module. Refer to the [official quickstart docs](https://yamllint.readthedocs.io/en/stable/quickstart.html) for details.

- Any platform (pip): `pip install yamllint`
- macOS (Homebrew): `brew install yamllint`
- Debian/Ubuntu: `sudo apt install yamllint`

Run it on a file

```bash
yamllint assets/code/sample-config.yaml
```

Common rules to enable or check

- indentation: spaces count (usually 2)
- line-length: keep lines reasonably short
- truthy: prefer `true`/`false` (lowercase) for booleans

Quick example: Check all YAML files in the repo

```bash
yamllint .
```

That's it — you now know enough YAML to read, write, and validate real-world config files. 🎉
