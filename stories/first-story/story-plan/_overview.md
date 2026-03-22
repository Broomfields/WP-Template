---
title: "Story Plan — Overview"
_author_only: true
---

# Story Plan

My author workspace for this story. Everything here is private — none of it ends up in the wiki or goes anywhere public. This is where I figure out what's happening, why it matters, and how I'm going to tell it. The wiki documents the world as it exists; this folder documents the story I'm telling within it.

---

## What Lives Here

### Root documents

The files at the root of `story-plan/` capture the overall shape of the story before it breaks down into arcs and chapters:

| File | Purpose |
|------|---------|
| `00-premise.md` | The core premise: the central question, the inciting situation, the stakes. The one-paragraph version of what the story is about. |
| `01-structure.md` | The overall narrative shape: how many arcs, what the broad movement is, where the story begins and ends emotionally and plot-wise. |
| `02-prose-style.md` | Voice, POV, tense, tone, and stylistic reference points. The touchstone to come back to when I'm drafting and losing the thread. |
| `reader-knowledge.md` | A high-level map of what the reader learns and when — looser than the `revelations/` subfolder, useful for early planning before I want to get too granular. |

### Subfolders

Each subfolder covers a specific planning category. Every one has its own `_overview.md` (explaining what goes in it) and a `_template.md` (ready to copy when making a new entry):

| Subfolder | What it tracks |
|-----------|---------------|
| `arcs/` | High-level narrative phases — opening state, closing state, thematic focus, linked wiki events |
| `characters/` | Story-specific notes for wiki characters: goals, arc journeys, key decisions, knowledge states |
| `locations/` | Narrative role of wiki locations within this story: atmosphere, scenes set there, symbolic weight |
| `themes/` | Individual thematic threads from introduction to resolution |
| `relationships/` | Story-critical character dynamics and how they evolve |
| `revelations/` | Individual reader and character knowledge reveals, queryable and sortable by arc and chapter |
| `objects/` | Story-significant items whose narrative role goes beyond their wiki entry |

---

## How This Relates to the Wiki

The story plan references the wiki. The wiki never references the story plan — that's the rule, and it matters.

When a story plan file needs to point to a wiki entry — a character, a location, an event, an object — it uses an Obsidian wikilink in a dedicated frontmatter field (`wiki_entry`, `wiki_events`, `characters`, etc.). The wiki entry carries no story metadata back.

If something that happens in this story changes a world-fact, update the wiki entry to reflect that. The wiki stays the source of truth for what the world *is*. This folder is for what the story *does with* that world.
