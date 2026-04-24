# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Local development
bundle exec jekyll serve

# Build and deploy to production
bash deploy.sh
```

`deploy.sh` runs `jekyll clean && jekyll build` then rsyncs `_site/` to `cerami@libra.dfci.harvard.edu:/webhomes/ksystems`.

## Architecture

Static Jekyll site for the Knowledge Systems Group (KSG) at Dana-Farber Cancer Institute.

- **Base URL**: `/knowledge-systems/` (hardcoded in links throughout)
- **`_config.yml`**: site title, baseurl, permalink pattern (`/:year/:month/:title`), includes `_pages/`
- **Layout chain**: `_pages/*.markdown` → `layout: page` → `_layouts/page.html` (adds `<h1>` + breadcrumbs + `.page-content` wrapper) → `_layouts/default.html` (Bootstrap container, navbar, footer)
- **Styling**: single file `css/styles.css` — no SASS compilation active despite `_sass/` directory existing. All custom styles live here.
- **Dependencies**: Bootstrap 5.3.0-alpha1 and Inter font via CDN (no npm/bundler for JS/CSS).

### Key files

| File | Purpose |
|---|---|
| `_includes/head.html` | Meta, fonts, Bootstrap CDN |
| `_includes/navigation.html` | Sticky navbar; active state via `page.url` Liquid checks |
| `_includes/breadcrumbs.html` | Auto-generated breadcrumbs included in `page` layout |
| `_includes/footer.html` | Footer outside `.container` |
| `css/styles.css` | All custom styles with CSS custom properties |

### Pages

All content pages live in `_pages/` with `layout: page` and a `permalink:` in their front matter. Navigation links to: Home (`index.markdown`), Projects, Team, Publications.

### Design system

CSS custom properties in `:root` (see `css/styles.css`):
- `--accent: #2563eb` (blue), `--text: #0f172a`, `--text-body: #334155`, `--text-muted: #64748b`
- `--surface: #f8fafc`, `--border: #e2e8f0`

Reusable component classes: `.team-grid` / `.team-card`, `.pub-list` / `.pub-card`, `.feature-grid` / `.feature-card`, `.platform-card`, `.home-news`, `.detail-lead`, `.project-tag` (`.tag-data`, `.tag-clinical`, `.tag-infra`).

Avatar colors cycle through `.av-1` through `.av-6` (blue, purple, cyan, green, amber, pink).
