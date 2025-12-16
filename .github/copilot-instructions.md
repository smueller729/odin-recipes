<!-- Guidance for AI coding agents working on the `odin-recipes` static site -->
# Odin Recipes — Copilot Instructions

This repository is a small static website (plain HTML) that lists a few recipe pages. There are no build tools, package managers, or tests. The goal of these instructions is to help an AI coding agent be productive immediately by describing the project's structure, conventions, and common edit patterns.

**Project Layout:**
- `index.html`: Root landing page. Links to recipe pages using `href="recipes/<name>.html"`.
- `recipes/`: Contains individual recipe pages (e.g., `butterchicken.html`, `lambkorma.html`). Use this folder for new recipe pages.
- `README.md`: Short project description.
- image files: occasionally placed at repo root (e.g., `lamb-korma2-1024x1536.jpg`) or referenced via external URLs inside recipe pages.

**Big-picture architecture / why it is structured this way**
- Simple, file-based static site. Each recipe is a standalone HTML file with its own markup and local links back to the home page (`<a href="../index.html">Home</a>`).
- No CSS/JS frameworks — keep edits limited to HTML unless adding assets intentionally.

**Common developer workflows**
- Preview: Double-click `index.html` in OS or run a local static server for more accurate testing:

  ```pwsh
  # from repository root
  python -m http.server 8000
  # then open http://localhost:8000 in a browser
  ```

- Add a new recipe: duplicate `recipes/butterchicken.html` as a template, update the `<title>`, headings, and relative link back to `../index.html`. Then add a link from `index.html`:

  ```html
  <a href="recipes/newrecipe.html">My New Recipe</a>
  ```

- Images: prefer external CDN links already used in recipes; if adding local images, store them in the repository root or a new `assets/` folder and reference them with a path relative to the HTML file (e.g., `../assets/image.jpg` or `../lamb-korma2-1024x1536.jpg`).

**Project-specific conventions & patterns**
- Recipe pages use the same HTML skeleton (doctype, `<meta viewport>`, `<title>`, one `<h1>`, `Home` link). Reuse that skeleton when adding pages.
- Links from `index.html` to recipes use `recipes/<name>.html`. Links from inside `recipes/` back to home use `../index.html`.
- Keep filenames simple and lowercase (existing pages: `butterchicken.html`, `lambkorma.html`). Use hyphens for multiword filenames if needed.

**Integration points & external dependencies**
- No build system or external dependencies. Recipe images are sometimes referenced from external sites (e.g., `mightymrs.com`, `chilipeppermadness.com`). Treat those as remote assets — validate URLs when updating.

**Editing & PR guidance for AI agents**
- Make minimal, focused changes: when adding a page, add the new file under `recipes/` and update `index.html` to add a link.
- Preserve the existing relative-link pattern. Example: a recipe page `recipes/x.html` should contain `<a href="../index.html">Home</a>`.
- If updating images, prefer adding to `assets/` (create it) and update paths consistently.
- Tests/build: none. Running a local static server (see preview section) is the recommended way to verify changes.

**Examples from this repo**
- Home links: `recipes/butterchicken.html` contains `<a href="../index.html">Home</a>`.
- Index links: `index.html` contains `<a href="recipes/butterchicken.html">Indian Butter Chicken</a>`.
- Local image present: `lamb-korma2-1024x1536.jpg` at the repo root (file naming is inconsistent with HTML-only images; consider `assets/` if adding more images).

If anything here is unclear or you want additional rules (naming conventions, commit message style, or an `assets/` migration), tell me which area to expand and I will update this file.
