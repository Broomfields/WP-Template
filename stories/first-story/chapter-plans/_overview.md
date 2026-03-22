---
title: "Chapter Plans — Overview"
_author_only: true
---

# Chapter Plans

Chapter plans are where the story plan meets the page. Each file in this folder covers a single chapter in detail — the scenes within it, what needs to happen, how it opens and closes, what the reader experiences, and what each POV character is doing and feeling. Chapter plans sit between the arc-level planning (which sets direction) and the actual prose (which delivers it).

A chapter plan isn't a summary written after the fact. It's a working document I write *before* drafting begins — a blueprint that lets me draft with confidence, knowing where I'm going and why.

---

## What an Entry Represents

One chapter plan file = one chapter. The file captures:

- **Scene breakdown** — what scenes the chapter contains, in order, with brief descriptions of what happens in each
- **Arc and sequence** — which narrative arc this chapter belongs to and its chapter number
- **POV** — whose perspective the chapter is told from
- **Opening and closing state** — where the chapter begins and ends (plot, character, tension)
- **Key beats** — the moments that must land: revelations, decisions, confrontations, turns
- **Reader knowledge** — what the reader learns or suspects by the end
- **Character knowledge** — what characters know, discover, or conceal
- **Tone and pacing** — the emotional register and rhythm of the chapter
- **Prose notes** — anything specific to keep in mind while drafting: a line to hit, an image to use, a rhythm to sustain

---

## Naming Convention

Files use the format `chapter-XX.md` where `XX` is the zero-padded chapter number: `chapter-01.md`, `chapter-02.md`, and so on. This keeps them in natural sort order in the file browser.

---

## How Entries Relate to the Rest of the System

- Each chapter plan references its primary story arc using the arc ID string (e.g. `arc: "story-01"`) in frontmatter — a plain string label, not a wikilink
- Character arcs and thematic arcs with significant presence in the chapter are listed in `featured_arcs: ["char-keva-01"]` — also plain string IDs
- Wiki entries referenced within a chapter are linked via Obsidian wikilinks in the body, not in frontmatter
- The story dashboard reads chapter plans to display the chapter summary table
- Chapter plans inform the prose files in `chapters/` but don't link to them directly

---

> Use [[_template]] to create a new chapter plan.
