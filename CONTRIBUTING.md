Contributing

Thank you for helping make this bundle friendly for beginners. Please follow the guidelines below when contributing content, images, or code.

1. Write for beginners
   - Use plain language and short sentences.
   - Define any jargon the first time it appears.
   - Prefer concrete, annotated examples over long theory.

2. Files and locations
   - Content markdown files: content/*.md
   - Images (figures/screenshots): assets/images/*
   - Example YAML files and code: assets/code/*

3. Images
   - Use descriptive file names (e.g., yaml-anchors-diagram.svg).
   - Include alt text when referencing images in markdown.
   - Path matters: files in `content/*.md` must link images as `../assets/images/...` (one level up), not `assets/images/...` — otherwise the image 404s on GitHub. Files at the repo root (like `README.md`) use `assets/images/...` directly.
   - Prefer SVG for diagrams; keep screenshots at reasonable resolution.

4. Code samples
   - Keep runnable examples small (<= 100 lines when possible).
   - Put full example files in assets/code and reference them from content.
   - Use comments in example YAML files to explain non-obvious lines.

5. Style
   - Use headings, bullet lists, and short code blocks to make content scannable.
   - Add a simple exercise at the end of each lesson.

6. Pull requests
   - Make a branch for your change and open a PR against main.
   - In the PR description, summarize the change and list any new files added.

7. Accessibility
   - Add alt text for all images.
   - Ensure code examples use a monospaced font (GitHub will render code blocks correctly).

Thanks for helping keep this bundle friendly, accurate, and fast to read!