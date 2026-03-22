---
title: "Story Plan Dashboard"
_author_only: true
---

# Story Plan Dashboard

> Author-only. Not pushed to the CMS.

```dataviewjs
const base = dv.current().file.folder;
```

---

## Arcs

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/arcs"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => {
    const ta = String(a.type ?? ""), tb = String(b.type ?? "");
    if (ta !== tb) return ta.localeCompare(tb);
    return (a.sequence ?? 99) - (b.sequence ?? 99);
  });
dv.table(["Type", "ID", "Title", "Status"],
  pages.map(p => [p.type ?? "—", p.id ?? "—", p.file.link, p.status ?? "—"]));
```

---

## Characters

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/characters"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => String(a.role ?? "").localeCompare(String(b.role ?? "")));
dv.table(["Name", "Wiki Entry", "Role", "Arc Introduced"],
  pages.map(p => [p.file.link, p.wiki_entry, p.role, p.arc_introduced ?? "—"]));
```

---

## Locations

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/locations"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => String(a.arc_introduced ?? "").localeCompare(String(b.arc_introduced ?? "")));
dv.table(["Name", "Wiki Entry", "Narrative Role", "Arc Introduced"],
  pages.map(p => [p.file.link, p.wiki_entry, p.narrative_role ?? "—", p.arc_introduced ?? "—"]));
```

---

## Themes

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/themes"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => String(a.arc_introduced ?? "").localeCompare(String(b.arc_introduced ?? "")));
dv.table(["Theme", "Arc Introduced"],
  pages.map(p => [p.file.link, p.arc_introduced ?? "—"]));
```

---

## Relationships

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/relationships"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => String(a.arc_introduced ?? "").localeCompare(String(b.arc_introduced ?? "")));
dv.table(["Relationship", "Type", "Characters", "Arc Introduced"],
  pages.map(p => [p.file.link, p.relationship_type ?? "—", p.characters, p.arc_introduced ?? "—"]));
```

---

## Revelations

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/revelations"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => {
    const aa = String(a.arc ?? "");
    const ab = String(b.arc ?? "");
    if (aa !== ab) return aa.localeCompare(ab);
    return (a.chapter ?? 999) - (b.chapter ?? 999);
  });
dv.table(["Revelation", "Arc", "Chapter", "Type", "Wiki Entry"],
  pages.map(p => [p.file.link, p.arc ?? "—", p.chapter ?? "—", p.knowledge_type ?? "—", p.wiki_entry ?? "—"]));
```

---

## Objects

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/objects"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => String(a.arc_introduced ?? "").localeCompare(String(b.arc_introduced ?? "")));
dv.table(["Object", "Wiki Entry", "Narrative Role", "Arc Introduced"],
  pages.map(p => [p.file.link, p.wiki_entry ?? "—", p.narrative_role ?? "—", p.arc_introduced ?? "—"]));
```
