# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo-based blog called "Leslie Tech Notes". It is deployed to GitHub Pages at `https://leslieo2.github.io/` and uses the private `leslie-journal` theme in `themes/leslie-journal/`.

## Development Commands

```bash
# Start development server with drafts enabled
hugo server --buildDrafts --disableFastRender

# Build the site for production
hugo

# Create new content (post)
hugo new posts/my-new-post.md
```

Always run `hugo` before committing to verify a clean build with no errors or warnings.

## Architecture

### Template hierarchy

The HTML shell is `themes/leslie-journal/layouts/_default/baseof.html`, which uses Hugo blocks (`favicon`, `head`, `header`, `main`, `footer`) so child templates can inject or override sections. The key override chain:

- **Homepage**: `themes/leslie-journal/layouts/index.html` defines `"main"` → structured as "chapters" (hero, intro from `_index.md`, recent posts grid, closing thought)
- **Single post**: `themes/leslie-journal/layouts/_default/single.html` defines `"header"` and `"main"` → article hero + body + tags + contextual sidebar
- **Section listing** (e.g., /posts/): `themes/leslie-journal/layouts/_default/list.html` → archive header + post cards + pagination
- **Summary card**: `themes/leslie-journal/layouts/_default/summary-with-image.html` — used for list items with optional featured images

### Partials and their responsibilities

| Partial | Purpose |
|---|---|
| `site-style.html` | Minifies and fingerprints the local site CSS via Hugo pipes |
| `site-scripts.html` | Mermaid.js rendering + Plausible analytics (supports both custom script URL and standard domain config) |
| `site-header.html` | Custom journal-branded header with nav menu |
| `site-footer.html` | Custom journal-branded footer |
| `site-favicon.html` | SVG favicon from `Site.Params.favicon` |
| `head-additions.html` | Google Fonts preconnect + stylesheet (Inter + Newsreader) |
| `seo.html` | Open Graph, Twitter Cards, Schema.org JSON-LD (Article, BreadcrumbList, Blog, Person, WebSite), canonical URL, pagination `rel=prev/next` |
| `reading-time.html` | CJK-aware reading time: uses character count / 450 for CJK content, otherwise word count / reading speed |
| `tags.html` | Renders tag links for a page |

### Configuration (`hugo.toml`)

Key params beyond the obvious:
- `params.hero` — drives the homepage hero section (title, labels, URLs, image)
- `params.plausibleCustomScriptURL` / `params.plausibleDomain` — analytics (custom script takes precedence)
- `params.body_classes` — sets the `<body>` class (currently `"theme-journal bg-near-white"`)
- `params.og_image` — fallback Open Graph image
- `menu.main` — nav items; the header marks the current page with `.is-active`

### Content patterns

- Posts use TOML front matter (`+++`). Supported fields: `title`, `date`, `draft`, `slug`, `tags`, `categories`, `description`, `images` (array for OG image), `copyright`
- Filenames in `content/posts/` use kebab-case
- Homepage intro content lives in `content/_index.md`
- Open-source projects are in `data/projects.yaml` (sections: `authored` and `contributed`)

### Styling conventions

The custom CSS uses a `journal-*` BEM-like namespace (e.g., `journal-home`, `journal-post-card`, `journal-article__body`). Site CSS lives in `themes/leslie-journal/assets/css/site.css`.

## Design constraints

- Do not edit files in `public/` or `resources/` — these are generated
- The deployment workflow (`.github/workflows/hugo.yml`) builds with `hugo --minify` and pushes `public/` to `leslieo2/leslieo2.github.io` via `peaceiris/actions-gh-pages`
- Reading time is CJK-aware: CJK posts estimate based on character count rather than word count
