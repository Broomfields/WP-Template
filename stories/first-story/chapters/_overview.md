---
title: "Chapters — Overview"
_author_only: true
---

# Chapters

This is where the actual prose lives — the words the reader sees. Each file is one chapter, drafted and revised here. The chapter plans in `chapter-plans/` are the blueprint; the files here are the build.

---

## What an Entry Represents

One file = one chapter of prose. The file contains:

- **Frontmatter** — a small set of metadata for tracking status and sequence
- **The prose itself** — the full drafted text of the chapter

Nothing else belongs here. Notes, plans, and structural thinking live in `chapter-plans/`. World context lives in `world-building/`. This folder is for writing.

---

## Naming Convention

Files use the same format as their corresponding chapter plan: `chapter-XX.md` where `XX` is the zero-padded chapter number. `chapter-01.md` in `chapters/` corresponds to `chapter-01.md` in `chapter-plans/`.

---

## Status Tracking

The `status` frontmatter field tracks where a chapter is in the drafting process. Suggested values:

| Value | Meaning |
|-------|---------|
| `outline` | Placeholder file — no prose yet |
| `draft` | First draft written, not yet revised |
| `revised` | Substantially revised, approaching final |
| `final` | Chapter is complete |

---

> Use [[_template]] to create a new chapter file.
