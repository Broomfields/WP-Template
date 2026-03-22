---
title: "Arcs — Overview"
_author_only: true
---

# Arcs

Arcs are the high-level narrative phases of the story — sitting between the root structure docs (which define the overall shape and premise) and the chapter plans (which get into the scene-by-scene detail). Each arc is a distinct phase with its own thematic focus, opening and closing state, and internal momentum.

Worth noting: arcs aren't the same thing as wiki time periods. A time period is a span of in-world history. An arc is a narrative construct — it might span one time period or several, and it's defined by the story's shape, not the world's calendar.

## What an Entry Represents

One arc entry = one narrative phase of the story. It covers what state the world and characters are in when the arc begins, what changes during it, what the reader is experiencing, and where things land when it closes. It also tracks which wiki events fall within this arc and what reader knowledge is introduced.

## How Entries Relate to the Rest of the System

- Arc files list the wiki events that occur within them via wikilinks in `wiki_events` — the story references the wiki, never the reverse
- Story character and location files reference arcs by ID in their frontmatter
- Chapter plans reference an arc by ID to indicate which narrative phase they belong to
- Revelation entries reference an arc by ID to track when knowledge is surfaced

## Arc Types

Arcs are typed. The `type` field distinguishes between three kinds:

| Type | Purpose | ID pattern | Example |
|------|---------|------------|---------|
| `story` | The main narrative phases — the primary structural divisions of the story | `story-{nn}` | `story-01`, `story-02` |
| `character` | A specific character's internal journey through the story, which may span multiple story arcs | `char-{name}-{nn}` | `char-keva-01`, `char-keva-02` |
| `thematic` | A thematic strand with a chronological development — introduction, complication, resolution | `theme-{name}-{nn}` | `theme-redemption-01` |

A character can have multiple arcs if their journey has distinct phases. Same with themes. The numeric suffix handles this in all three types.

Character arc entries include a `character` field: an Obsidian wikilink to the corresponding story-plan character file (not the wiki entry). This keeps character arcs navigable from both directions.

## Linking Convention

Arc IDs are plain string labels — not wikilinks. Other story-plan files reference arcs using these IDs in frontmatter.

- Chapter plans use `arc: "story-01"` for their primary arc and `featured_arcs: ["char-keva-01"]` for any character or thematic arcs with significant presence in that chapter.
- Character and revelation files use `arc_introduced` to note which arc first introduces them, using the relevant arc ID.

Wiki events are linked from the arc file using Obsidian wikilinks in the `wiki_events` array: `wiki_events: ["[[event-slug]]"]`. The wiki event itself carries no story metadata — the arc file is the sole record of where that event sits in the narrative.

---

> Use [[_template]] to create a new arc entry.
