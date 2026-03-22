---
title: "Characters — Overview"
_author_only: true
---

# Characters

The wiki holds the canonical definition of every character: their history, abilities, relationships, appearance, and role in the world. These story character files are different — they capture what a character's presence *means specifically within this story*. Goals, wounds, arc journeys, key decisions, knowledge states. That stuff is story-specific and lives here, not cluttering up the world encyclopedia.

Not every wiki character needs a file here. Only those with meaningful presence in this story — the ones whose choices, growth, or relationships actually drive or significantly affect the plot.

## What an Entry Represents

One entry covers one character's story-specific notes: why they're in this story, what they want, what's holding them back, how they change across arcs, and what they know and when. The wiki entry remains the canonical source of world-truth. This file is story-truth.

## How Entries Relate to the Rest of the System

- Each entry links to the character's wiki entry via the `wiki_entry` frontmatter field (Obsidian wikilink)
- Entries reference arcs by ID to track when the character is introduced and active
- Relationship entries link to characters via wikilinks in their `characters` array
- The story dashboard surfaces all story characters and their roles

## Linking Convention

Use an Obsidian wikilink in the `wiki_entry` field: `wiki_entry: "[[character-slug]]"`. This makes the connection navigable and visible in the graph. Name this file using the same slug as the wiki character entry for clarity — e.g. `kira-ashenvale.md` links to `[[kira-ashenvale]]`.

---

> Use [[_template]] to create a new story character entry.
