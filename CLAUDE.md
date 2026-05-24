# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Local development (live reload at http://localhost:1313)
hugo server

# Include draft posts during development
hugo server -D

# Production build (same as CI)
hugo --minify

# Create a new post from archetype
hugo new posts/<slug>.md
```

No npm, webpack, or other build tooling — Hugo CLI is the only dependency.

## Architecture

This is a Hugo static site using the **PaperMod** theme, deployed to GitHub Pages via GitHub Actions.

- **`hugo.yaml`** — single config file; no `config/` directory split
- **`content/posts/`** — project articles (portfolio entries)
- **`content/about.md`** — standalone profile page
- **`static/`** — maps directly to site root; images in `static/images/`, videos in `static/videos/`
- **`themes/PaperMod/`** — theme vendored as a regular folder, not a git submodule
- **`layouts/shortcodes/video.html`** — custom shortcode for MP4 embeds
- **`public/`** — build output, gitignored, never commit

The homepage uses PaperMod's `homeInfoParams` mode (configured in `hugo.yaml`). Menu items are also defined in `hugo.yaml` under `menu.main`.

## Content authoring

**New post frontmatter** (from archetype):
```yaml
---
title: "..."
date: <date>
tags: []
summary: ""
draft: true   # change to false to publish
---
```

- Cover image: path in frontmatter is relative to `static/` — e.g., `image: "images/foo/cover.png"` resolves to `static/images/foo/cover.png`
- Video embed: `{{< video src="/videos/filename.mp4" >}}`
- Standalone pages (like `about.md`) need `layout: "page"` and an explicit `url:` in frontmatter

## Deployment

Push to `main` → GitHub Actions builds with Hugo 0.160.1 extended → deploys to GitHub Pages automatically. No manual step needed. The workflow is at `.github/workflows/deploy.yml`.
