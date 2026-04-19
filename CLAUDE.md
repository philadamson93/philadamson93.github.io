# CLAUDE.md

## Before You Do Anything

**Read `docs/claude_ops.md` for operating standards.** This file is adapted from the VISTA and paper-trail `claude_ops.md`. Site-specific conventions (deployment, content vs. theme changes, when planning is required) are defined there.

---

## Project Overview

Personal website for Philip M. Adamson. Static site built with [al-folio](https://github.com/alshedivat/al-folio) (Jekyll). Deployed via GitHub Pages from `main`.

## Key Entry Points

- `_config.yml` — site config (title, URL, nav, plugin options)
- `_data/socials.yml` — social links and identifiers
- `_pages/about.md` — home page (landing)
- `_posts/` — blog posts
- `_bibliography/papers.bib` — publications (BibTeX)
- `docs/claude_ops.md` — operating standards
- `docs/plans/` — planning docs for non-trivial changes

## Local Development

```bash
bundle install           # first time only
bundle exec jekyll serve # http://localhost:4000
```

## Upstream Theme Docs

The al-folio theme ships its own `AGENTS.md`, `QUICKSTART.md`, `CUSTOMIZE.md`, `INSTALL.md`, `FAQ.md`, and `TROUBLESHOOTING.md`. Consult these for theme-specific questions; they describe upstream features, not this site's operating standards.
