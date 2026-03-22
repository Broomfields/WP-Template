---
title: "System Overview"
_author_only: true
---

# System Overview

My reference for how this whole thing fits together: the rules, the conventions, and why I set things up the way I did. If I'm about to make a structural change, add a new entity type, or I've come back after six months with absolutely no idea why any of this looks the way it does, I start here.

---

## Repository Structure

```
/
├── world-building/
│   └── wiki/                  ← world encyclopedia (see The Wiki)
│       ├── _dashboard.md      ← master wiki dashboard
│       └── [entity folders]/  ← one folder per entity type
├── stories/
│   └── [story-name]/          ← one folder per story
│       ├── _dashboard.md      ← story-level dashboard
│       ├── story-plan/        ← narrative planning (see The Story Plan)
│       ├── chapter-plans/     ← one file per chapter
│       └── chapters/          ← prose files
└── _system-overview.md        ← this file
```

---

## The Wiki

### Purpose

My world encyclopedia — everything that exists in the world lives here: characters, locations, events, races, languages, cultures, all of it. Main thing to remember: it's written as if the story doesn't exist. It's about the world, not the narrative I'm telling within it.

### Who I'm Writing For

Wiki entries need to work for anyone at any point without assuming what they already know. That could be me mid-draft needing a quick reference, a reader who's finished the first story and wants to dig deeper, or someone mid-story just checking a detail. So no spoilers, no framing things through story events, no assuming the reader knows how a particular arc ends.

### Entity Types

Each entity type gets its own subfolder under `world-building/wiki/`. Every entry has an `entity` field in frontmatter for the type, and a `type` field for the subtype. Current types:

`character` · `location` · `event` · `time-period` · `race` · `group` · `lore` · `object` · `environment` · `societal-system` · `language` · `culture` · `fauna` · `flora` · `fungus` · `technology` · `magic` · `cosmology`

### Relationship Rule: Child References Parent

In any hierarchical relationship, **the child holds the reference to the parent — not the other way round**. A child entry has a `parent_location`, `parent_period`, or `parent_race` field; the parent says nothing.

Adding a new child never requires touching an existing parent entry. I find children by querying: "give me everything whose `parent_location` is X" — not by maintaining a list that'll go stale the moment I forget to update it.

Siblings and spouses are the natural exception since those are mutual, so both sides reference each other. There may be a few other spots where I've broken the rule because it felt right, but child-references-parent is what I'm working to.

### The Wiki Doesn't Reference the Story Plan

Wiki entries don't reference the story plan. They don't know which arc they're in, what narrative role they're playing, or how a story uses them. That all lives in the story plan.

The one exception is `first_revealed` — a CMS field that tells the pipeline when this entry becomes visible to readers. It's not pointing at the story plan; it's a publication control. The wiki still has no idea it's in a story.

If it feels like a wiki entry needs story context — like "this character is the antagonist in story one" — that belongs in the story plan, pointing outward to the wiki. Once wiki entries start annotating themselves with narrative roles, both systems get harder to work with.

### Frontmatter Conventions

Wiki entries use two kinds of frontmatter fields:

**Content fields** — the world-facts: `title`, `entity`, `type`, `summary`, `status`, `aliases`, `first_revealed`, relationships to other entries, and so on.

**Author-only fields** — prefixed with an underscore (`_`). Never exported, never reader-facing, purely for my own use. The ones I use:

| Field            | Type    | Purpose                                                                                                       |
| ---------------- | ------- | ------------------------------------------------------------------------------------------------------------- |
| `_author_only`   | boolean | If `true`, this entry is never exported. Use for dashboards, templates, and anything not ready for public eyes. |
| `_status`        | string  | My view of this entry's completeness. Values: `draft`, `active`. Separate from the in-world `status` field.   |
| `_priority`      | string  | Flags entries that need attention. Values: `high`, `medium`, `low`.                                           |
| `_review_needed` | boolean | Something needs reconsidering, verifying, or reworking.                                                       |
| `_todo`          | array   | Outstanding tasks for this specific entry.                                                                    |
| `_notes`         | array   | Informal notes that don't belong in the entry's actual content.                                               |

The underscore isn't just decorative. Obsidian's Dataview plugin doesn't expose underscore-prefixed YAML keys through standard DQL, so every dashboard runs as DataviewJS, which reads raw frontmatter directly via `page.file.frontmatter["_field"]` and gets around that entirely.

### Dashboards

Each entity folder has a `_dashboard.md` in DataviewJS, author-only and never exported. It gives me:

- A summary count of entries in that category
- Breakdowns by type and status
- Filtered views: drafts, high-priority, flagged for review, open TODOs
- Missing required fields — entries where mandatory frontmatter is absent

The master dashboard at `world-building/wiki/_dashboard.md` pulls all of that together across every entity type.

### Meta Files

Each entity folder also has:

- `_overview.md` — explains what this entity type is and how to use it
- `_template.md` — a ready-to-copy frontmatter and section structure for new entries

Both get filtered out of dashboard queries by checking `file.name !== "_overview" && file.name !== "_template"`.

---

## The Story Plan

### Purpose

My narrative workspace. Most of this is purely author-facing — the planning documents, dashboards, and chapter plans are mine and never leave the repo. The exception is the `chapters/` folder, which holds the actual prose. Completed chapters get picked up by the CMS; everything else doesn't. The wiki covers the world; the story plan covers the story I'm telling within it.

### Structure

Each story lives in `stories/[story-name]/` and contains:

```
[story-name]/
├── _dashboard.md              ← arc overview and chapter plan summary
├── story-plan/
│   ├── _dashboard.md          ← planning dashboard across all categories
│   ├── 00-premise.md          ← core premise and central question
│   ├── 01-structure.md        ← overall narrative shape and arc sequence
│   ├── 02-prose-style.md      ← voice, POV, tone, and style reference
│   ├── reader-knowledge.md    ← high-level map of what the reader learns
│   ├── arcs/                  ← one file per narrative arc
│   ├── characters/            ← story-specific notes for wiki characters
│   ├── locations/             ← story-specific notes for wiki locations
│   ├── themes/                ← thematic threads and their development
│   ├── relationships/         ← story-critical character dynamics
│   ├── revelations/           ← individual reader/character knowledge reveals
│   └── objects/               ← story-significant items
├── chapter-plans/             ← one file per chapter
└── chapters/                  ← prose files; completed chapters picked up by CMS
```

Each subfolder has its own `_overview.md` explaining what goes there and a `_template.md` to copy from.

### Story Plan Categories

**Arcs** are the high-level narrative sections of the story, sitting above chapter plans and below the root structure docs. Each arc file covers the type, sequence, opening and closing state, thematic focus, and which wiki events fall within it. Three types:

| Type        | Tracks                                                              | ID pattern              |
| ----------- | ------------------------------------------------------------------- | ----------------------- |
| `story`     | Primary narrative phases of the story                               | `story-01`, `story-02`  |
| `character` | A specific character's internal journey through the story           | `char-[name]-01`, `char-[name]-02` |
| `thematic`  | A thematic strand with a chronological development                  | `theme-[name]-01`       |

Characters can have multiple character arcs across distinct phases; themes can have multiple thematic arcs. The numeric suffix handles this in all three types.

**Characters** capture story-specific notes for characters with meaningful presence in this story: goals, internal conflicts, arc journeys, key decisions, knowledge states. Stuff that belongs here, not in the wiki. Each file links to the corresponding wiki character entry.

**Locations** capture the narrative role of wiki locations within this story: why they're there, how they should feel in prose, the scenes set there, any symbolic weight they carry. Each file links to the corresponding wiki location entry.

**Themes** track individual thematic threads from introduction to resolution: the question each theme poses, which characters carry it, and how it develops arc by arc.

**Relationships** cover story-critical dynamics between characters: starting state, how they evolve, the key turning points, where they end up.

**Revelations** map the information architecture of the story: what gets revealed to the reader, what gets revealed to characters, and whether any gap between the two creates tension or dramatic irony. Making each revelation a queryable entry means I can surface the full picture of how reader understanding builds, and where I'm running ahead of or behind the characters.

**Objects** cover story-significant items whose narrative role goes beyond their wiki entry: MacGuffins, symbolic objects, things that change hands or carry thematic weight.

---

## Cross-System Rules

How the wiki and story plan talk to each other — and more importantly, how they don't. The idea is keeping both clean enough that I can work on either one without accidentally breaking the other.

### 1. The story plan references the wiki, not the other way round.

Most important rule in here. Wiki entries don't reference the story plan — anything about how a story uses them goes in the story plan, pointing outward to the wiki. (`first_revealed` is the one exception — it's a CMS publication flag, not a story plan reference.)

### 2. Wiki events are linked from arc files, not tagged on wiki entries.

Wiki events for an arc go in the arc file's `wiki_events` field as Obsidian wikilinks. The story dashboard reads those and pulls up the wiki pages. The wiki event doesn't reference the story plan.

### 3. Story-plan links to wiki entries use Obsidian wikilinks.

When a story plan file references a wiki entry — a character, a location, an event, an object — it does so via an Obsidian wikilink in a dedicated frontmatter field (`wiki_entry`, `wiki_events`, `characters`, etc.). Keeps everything navigable and queryable within Obsidian.

### 4. Arc IDs are plain string labels following a typed naming scheme.

Arc IDs use plain strings rather than wikilinks. The naming convention bakes the arc type into the ID so it's self-describing:

- Story arcs: `story-01`, `story-02`
- Character arcs: `char-[name]-01`, `char-[name]-02`
- Thematic arcs: `theme-[name]-01`

Chapter plans reference their primary arc with `arc: "story-01"`. Character and thematic arcs with significant presence in the chapter go in `featured_arcs: ["char-[name]-01"]`. These are plain strings rather than wikilinks since arc files are internal to the story plan and don't need to resolve anywhere.

### 5. The wiki is the source of truth for world-facts.

If a character's background, a location's history, or a magic system's rules are in the wiki, that's the authoritative version. Story plan files can note how these things *function in the story*, but they don't redefine or contradict the wiki. If a story causes a world-fact to change (a character dies, a location gets destroyed, a piece of lore gets retconned), I update the wiki entry to match.

---

## Naming Conventions

All content files use **kebab-case**: lowercase, hyphen-separated. No underscores in content filenames, no spaces. It's URL-safe, plays nicely with the CMS pipeline, and doesn't cause the edge cases that spaces or mixed capitalisation tend to.

The only exception is the underscore on meta files: `_dashboard.md`, `_overview.md`, `_template.md`, `_system-overview.md`. That's intentional — it sorts them to the top of directory listings and makes it immediately obvious they're infrastructure, not content.

---

## A Note on DataviewJS

All dashboards here run on `dataviewjs`, not plain `dataview`. Reason being: Obsidian's Dataview plugin doesn't expose underscore-prefixed YAML keys (`_author_only`, `_status`, `_priority`, etc.) through standard DQL. Since my whole workflow depends on those fields, every query runs as DataviewJS, which reads raw frontmatter directly via `page.file.frontmatter["_field"]` and gets around that entirely.
