---
title: "Creating a simple YAML — use of VS Code"
---

# Creating a simple YAML — Using VS Code

Step-by-step: make your first YAML file

1. Install Visual Studio Code (VS Code) from https://code.visualstudio.com/ if you don't have it.
2. Open the Extensions view (Ctrl+Shift+X) and install the "YAML" extension (e.g., Red Hat YAML: `redhat.vscode-yaml`). This adds schema support, validation, and helpful autocompletion.
3. Create a new file and save it with the extension `.yaml` or `.yml` (for example `sample-config.yaml`).
4. Paste this simple example or open the provided example at `assets/code/sample-config.yaml`.

Basic VS Code tips for YAML

- Indentation matters: use 2 spaces (or your team's preference) and avoid mixing tabs.
- The YAML extension will underline syntax errors and show messages in the Problems panel.
- You can add a JSON Schema to get autocompletion for known keys (see Red Hat YAML extension docs).

Sample file you can open: `assets/code/sample-config.yaml`

Exercises

- Create `demo.yaml` and paste the example. Change values and save — notice how the Problems panel helps catch errors.
- Try converting a small JSON file into YAML by hand and check it with `yamllint` (see validation page).
