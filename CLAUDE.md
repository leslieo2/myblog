# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo-based blog called "Leslie Tech Notes" using the Ananke theme. The site is deployed to GitHub Pages at https://leslieo2.github.io/.

## Development Commands

### Local Development
```bash
# Start development server with drafts enabled
hugo server --buildDrafts --disableFastRender

# Build the site for production
hugo

# Create new content (post)
hugo new posts/my-new-post.md
```

### Content Management
- Posts are created in `content/posts/` directory
- Use `hugo new posts/post-name.md` to create new posts with proper front matter
- Posts start as drafts by default (set `draft: false` to publish)

## Architecture

### Theme Structure
- Uses the **Ananke** Hugo theme (`themes/ananke/`)
- Custom layouts override theme defaults in `layouts/` directory
- Theme configuration in `themes/ananke/config/_default/`

### Custom Layouts
- `layouts/index.html` - Homepage with open-source projects section
- `layouts/_default/single.html` - Single post layout with copyright notice
- `layouts/partials/site-footer.html` - Custom footer with contact email
- `layouts/partials/site-scripts.html` - Mermaid.js integration for diagrams

### Data Files
- `data/projects.yaml` - Open-source project listings (authored and contributed)
- Projects are displayed on the homepage in two columns

### Configuration
- Main config: `hugo.toml`
- Base URL: `https://leslieo2.github.io/`
- Theme: `ananke`
- Language: `en-us`

## Content Features

### Front Matter Fields
Posts support these front matter fields:
- `title`, `date`, `draft`, `tags`, `categories`, `description`, `copyright`
- Example: See `content/posts/context-engineering.md`

### Mermaid Diagrams
- Posts can include Mermaid diagrams using code blocks with `language-mermaid`
- Automatic rendering is handled by custom JavaScript in `site-scripts.html`

### Open Source Projects
- Homepage displays projects from `data/projects.yaml`
- Two sections: "Author" (projects created) and "Contributor" (projects contributed to)

## Deployment
- Site is built and deployed to GitHub Pages
- Production build excludes draft posts
- Base URL configured for GitHub Pages deployment