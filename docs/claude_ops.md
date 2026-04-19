# Claude Code Operating Standards

This document defines how Claude Code should operate in the `philipmadamson.github.io` repo. Reference this file at the start of every planning document.

Adapted from the VISTA `claude_ops.md` and the paper-trail variant. Site-specific differences noted inline.

---

## Core Principles

1. **Plan before you code.** Enter Plan mode (Shift+Tab twice) before any non-trivial change — theme overhauls, new sections, layout rework. Skip planning for writing a post or tweaking copy.
2. **Re-enter plan mode when direction changes.** If a new constraint or design concern surfaces mid-implementation, pause.
3. **A wrong fast answer is slower than a right slow answer.** Prioritize correctness over speed.
4. **You don't trust; you instrument.** For this repo, verification means building the site locally (`bundle exec jekyll serve`) and checking the page in a browser before calling a change done. Type-check and lint do not verify visual correctness.
5. **YAGNI.** Don't build for hypothetical futures. Implement what's needed now.

---

## Environment

- **Local code execution is allowed.** Jekyll + Ruby run on this machine.
- **Preview locally before committing visual changes.** `bundle exec jekyll serve` then open `http://localhost:4000`. For first-time setup run `bundle install`.
- **Deployment is automatic.** GitHub Pages rebuilds from `main` on push — so `main` is effectively production. Stage substantial changes on a branch.
- **Most "code" is content.** Markdown posts in `_posts/`, pages in `_pages/`, data in `_data/`, config in `_config.yml`. Theme internals (`_layouts/`, `_includes/`, `_sass/`) are Liquid + SCSS.

---

## Planning Workflow

### When a plan doc is warranted

- New top-level section or page type.
- Theme or layout overhaul.
- Migration off al-folio.
- Adding tooling (analytics, comments, search backends, build pipelines).

### When it isn't

- Writing or editing a post.
- Tweaking config fields, socials, or nav order.
- Copy edits.
- Minor SCSS adjustments.

### Starting a planned task

1. Enter Plan mode.
2. **Read the relevant theme files first.** al-folio conventions matter — check `_layouts/`, `_includes/`, `_sass/_base.scss`, `_config.yml` before proposing changes.
3. Draft the plan in plan mode's internal file.
4. Begin the plan doc with `Reference: docs/claude_ops.md`.
5. Articulate *what* and *why*.
6. Ask: "Are there any points of ambiguity about this plan?"
7. Iterate until solid, then exit plan mode.

### Saving the plan

1. Exit plan mode — this approves plan *content*, not implementation.
2. Copy to `docs/plans/<descriptive-name>.md` (not `plan_01.md`).
3. Stop and confirm before implementing.

### Plan Document Structure

```markdown
Reference: docs/claude_ops.md

# [Descriptive Task Title]

## Goal
What are we building and why?

## Approach
How will we implement this?

## Files to Modify / Create
- path/to/file.md — description of changes

## Open Questions
- Ambiguities still to resolve?

## Verification
How will we know this works? (For this repo: what page/route, at what viewport, and what should visually appear or not appear.)
```

### After completing a plan

- Update affected docs (`README.md`, cross-references in other plan docs).
- Mark the plan doc completed: `**Status: Completed** (date)` at the top.

---

## Code Quality Standards

### Re-use Over Duplication

- Prefer al-folio's existing includes and layouts over new ones. Most common things (pages, posts, news, profiles) already have a layout.
- Theme variables live in `_sass/_themes.scss` and `_sass/_variables.scss` — edit there rather than hard-coding colors/spacing inline.

### Simplicity

- Prefer a config tweak over a template override; a template override over a custom layout; a custom layout over forking theme internals.
- Don't add features that aren't explicitly requested.

---

## Git Practices

### Before Committing

- **Always check and report the current branch.** Confirm with the user if it seems unexpected.
- Since `main` auto-deploys, substantial visual changes belong on a feature branch first.

### Branching

- Content (posts, copy edits, config), minor style tweaks → `main`.
- New sections, theme refactors, layout changes → feature branch.

### Commit Messages

- **No AI attribution.** Never include `Co-Authored-By: Claude` or similar trailers.
- **One sentence, max.** Keep messages concise and descriptive. No body paragraphs unless the user explicitly asks.
- **One theme per commit.** Split config / content / theme changes into separate commits.

### Commit Frequency

- Commit frequently to maintain clean revert points.

---

## Communication Standards

### Ask Clarifying Questions For

- Content decisions (what to write, what to include in a bio, which posts to feature).
- Design/visual decisions that affect the site's identity (colors, typography, layout structure).
- Anything where assumptions could lead to wasted writing.

### Use Your Judgement For

- Prompt wording in draft copy (propose, don't commit).
- Internal file structure (where a new include lives, how a partial is named).
- Standard refactors within a single file.

---

## Pre-Commit Review Agents

Skip for content and minor theme tweaks. Run for non-trivial changes (new section type, theme refactor, tooling additions).

### Implementation Review Agent

Prompt template:
```
IMPORTANT: Follow docs/claude_ops.md. Your job is read-only review.

Review all changes in this session against the plan doc at docs/plans/<plan>.md. Check:
1. Do changes match the plan spec?
2. Were claude_ops procedures followed (plan doc saved, thematic commits, docs updated)?
3. Any code quality issues (YAGNI violations, unnecessary complexity, bypassed theme conventions)?
4. Is the Verification section addressable — did Claude actually load the page and check?
Report issues with specific file:line references.
```

---

## Context Management

- **Fresh sessions for fresh tasks.** Start new sessions when switching unrelated work (e.g., writing a post → theme refactor).
- **Match rigor to stakes.** A typo fix doesn't need plan mode; a theme overhaul does.
