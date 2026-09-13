---
title: "Creating a simple YAML — Using VS Code"
---

# Creating a simple YAML — Using VS Code

Step-by-step: make your first YAML file

1. Install Visual Studio Code (VS Code) from https://code.visualstudio.com/ if you don't have it.
2. Open the Extensions view (Ctrl+Shift+X) and install the "YAML" extension (e.g., Red Hat YAML: `redhat.vscode-yaml`). This adds schema support, validation, and helpful autocompletion.
3. Create a new file and save it with the extension `.yaml` or `.yml` (for example `sample-config.yaml`).
4. Paste this simple example or open the provided example at `assets/code/sample-config.yaml`.

Editors

YAML at its base is a text file and can be created and edited in any text editor. Popular editors include:

- Visual Studio Code (VS Code)
- Atom
- Notepad++

Tip: If using VS Code, install the Red Hat "YAML" extension (publisher: redhat) — it helps with linting, schema validation, and autocompletion.

File extensions

YAML files can use either `.yaml` or `.yml`. Both are equivalent; pick the convention your project prefers and stay consistent.

Points worth remembering (Rules for creating YAML files)

- YAML is case sensitive — `name` and `Name` are different keys.
- Use `.yaml` or `.yml` as the file extension.
- Do NOT use tab characters for indentation — use spaces only. The number of spaces doesn't matter as long as you are consistent (2 spaces is a common convention).
- Keep lines short and add comments with `#` to explain non-obvious values.

First example (placeholder names)

Let's create a simple example file and save it as `assets/code/examplecorp.yml` in this repository. The file describes a fictional company; we use neutral placeholder names so it's safe to share.

Example file (assets/code/examplecorp.yml):

```yaml
companyname: ExampleCorp
Type: Software
Founded: 1999
HeadQuarter: San Ramon, CA, USA
ParentOrganization: ParentCorp Ltd.
```

Notes

- Keys in YAML are case sensitive — `companyname` is different from `CompanyName`.
- Keep indentation consistent and do not use tabs.
- In a real project, choose a consistent key naming style (snake_case or camelCase) and stick with it.

Exercise

- Open VS Code, create `assets/code/examplecorp.yml`, paste the example above, save, and observe how the YAML extension gives syntax help. Try changing values and adding a comment using `#`.

When you're ready I can also:
- Add a `.yamllint` config to enforce beginner-friendly rules.
- Add a GitHub Action to run yamllint on pushes and PRs.
