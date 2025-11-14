# Repository Guidelines

This repository hosts the Hugo-powered blog **Leslie Tech Notes**, deployed to GitHub Pages.

## Project Structure & Module Organization

- `hugo.toml`: Main site configuration.
- `content/`: Markdown posts and pages (e.g., `content/posts/`).
- `layouts/`: Custom templates and partials that override the Ananke theme.
- `themes/ananke/`: Upstream theme; avoid modifying unless necessary.
- `data/`: Structured data (e.g., `data/projects.yaml` for homepage projects).
- `assets/`, `static/`: Styles, scripts, and static files.
- `public/` and `resources/`: Generated output and cache; do not edit by hand.

## Build, Test, and Development Commands

- `hugo server --buildDrafts --disableFastRender`: Run the local dev server with drafts enabled.
- `hugo`: Build the production site into `public/`.
- `hugo new posts/my-new-post.md`: Scaffold a new post with front matter.

Before opening a PR, run `hugo` and ensure there are no build errors or warnings.

## Coding Style & Naming Conventions

- Content files in `content/posts/` should use kebab-case filenames (e.g., `context-engineering.md`).
- Prefer clear, descriptive titles and `description` front matter.
- Use 2-space indentation in templates and YAML/JSON data.
- Keep custom layouts in `layouts/` rather than editing theme files when possible.

## Testing Guidelines

There is no dedicated automated test suite; validation is via Hugo:

- `hugo server --buildDrafts --disableFastRender` to preview changes locally.
- `hugo` to confirm a clean production build before merging.

## Commit & Pull Request Guidelines

- Write concise, imperative commit messages (e.g., `Add mermaid diagram to context post`).
- Keep PRs focused and small; include a short description of changes, affected paths, and any new commands.
- When changing layouts, mention impacted templates (e.g., `layouts/_default/single.html`).
- For visual changes, attach screenshots or describe key UI differences. 

## Agent-Specific Notes

Automated tools should avoid editing `public/`, `resources/`, and vendored theme files unless explicitly requested. Prefer edits to `content/`, `layouts/`, `data/`, and config.
