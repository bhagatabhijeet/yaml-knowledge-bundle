---
type: Guide
title: "Validating YAML using yamllint"
description: "Install and use yamllint to catch common YAML issues"
generated: { by: human:bhagatabhijeet, at: 2026-09-13T04:58:00Z }
---

# Validating YAML using yamllint

Why validate?

- Small mistakes (tabs, trailing spaces, bad indentation) can break YAML parsers.
- `yamllint` helps catch style and syntax issues early.

Install `yamllint`

- macOS (Homebrew): `brew install yamllint`
- Linux (pip): `pip install yamllint`
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

If you want, I can add a `.yamllint` config file to this repo with beginner-friendly rules (2-space indentation, allow long lines for examples). Ask and I'll add it.
