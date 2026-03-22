---
title: "Story Dashboard"
_author_only: true
---

# Story Dashboard

> Author-only. Not pushed to the CMS.

---

## Arc Overview

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/story-plan/arcs"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => {
    const ta = String(a.type ?? ""), tb = String(b.type ?? "");
    if (ta !== tb) return ta.localeCompare(tb);
    return (a.sequence ?? 99) - (b.sequence ?? 99);
  });
dv.table(["Type", "ID", "Arc", "Status"],
  pages.map(p => [p.type ?? "—", p.id ?? "—", p.file.link, p.status ?? "—"]));
```

---

## Wiki Events by Arc

```dataviewjs
const storyBase = dv.current().file.folder;

const arcs = [...dv.pages('"' + storyBase + '/story-plan/arcs"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => (a.sequence ?? 99) - (b.sequence ?? 99));

for (const arc of arcs) {
  dv.header(3, arc.title ?? arc.file.name);
  const linked = arc.wiki_events;
  const links = !linked ? [] : Array.isArray(linked) ? linked : [linked];
  if (links.length === 0) {
    dv.paragraph("_No wiki events linked to this arc yet._");
    continue;
  }
  const rows = links
    .map(link => dv.page(link.path ?? link))
    .filter(p => p != null)
    .sort((a, b) => String(a.world_date ?? "").localeCompare(String(b.world_date ?? "")))
    .map(p => [p.file.link, p.world_date ?? "—", p.type ?? "—"]);
  dv.table(["Event", "World Date", "Type"], rows);
}
```

---

## Chapter Plan Summary

```dataviewjs
const base = dv.current().file.folder;
const pages = [...dv.pages('"' + base + '/chapter-plans"')
  .where(p => p.file.name !== "_overview" && p.file.name !== "_template")]
  .sort((a, b) => (a.chapter ?? 999) - (b.chapter ?? 999));
if (pages.length === 0) {
  dv.paragraph("_No chapter plans yet._");
} else {
  dv.table(["Chapter", "Title", "Arc", "Featured Arcs", "Status"],
    pages.map(p => {
      const fa = p.featured_arcs;
      const featured = !fa ? "—" : Array.isArray(fa) ? fa.join(", ") : String(fa);
      return [p.chapter ?? "—", p.file.link, p.arc ?? "—", featured, p.status ?? "—"];
    }));
}
```
