---
title: "Events Dashboard"
_author_only: true
---

# Events Dashboard

> Author-only. Not pushed to the CMS.

---

## Summary

```dataviewjs
const pages = dv.pages('"world-building/wiki/events"')
  .where(p => !p.file.frontmatter["_author_only"] && p.entity === "event");
dv.table(["event", "Total"], [["event", pages.length]]);
```

---

## Breakdown by Type

```dataviewjs
const pages = dv.pages('"world-building/wiki/events"')
  .where(p => !p.file.frontmatter["_author_only"] && p.entity === "event");
const groups = {};
for (const p of pages) {
  const key = String(p.type ?? "(none)");
  groups[key] = (groups[key] ?? 0) + 1;
}
dv.table(["Type", "Count"],
  Object.entries(groups).sort(([a],[b]) => a.localeCompare(b)));
```

---

## Breakdown by Status

```dataviewjs
const pages = dv.pages('"world-building/wiki/events"')
  .where(p => !p.file.frontmatter["_author_only"] && p.entity === "event");
const groups = {};
for (const p of pages) {
  const key = String(p.status ?? "(none)");
  groups[key] = (groups[key] ?? 0) + 1;
}
dv.table(["Status", "Count"],
  Object.entries(groups).sort(([a],[b]) => a.localeCompare(b)));
```

---

## Draft Entries

```dataviewjs
const po = {high: 0, medium: 1, low: 2};
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => p.file.frontmatter["_status"] === "draft" && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => {
    const pd = (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99);
    return pd !== 0 ? pd : a.file.name.localeCompare(b.file.name);
  });
dv.table(["Type", "Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.status, p.file.frontmatter["_priority"], p.file.link]));
```

---

## Entries Flagged for Review

```dataviewjs
const po = {high: 0, medium: 1, low: 2};
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => p.file.frontmatter["_review_needed"] === true && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => {
    const pd = (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99);
    return pd !== 0 ? pd : a.file.name.localeCompare(b.file.name);
  });
dv.table(["Type", "_Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```

---

## High-Priority Entries

```dataviewjs
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => p.file.frontmatter["_priority"] === "high" && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => {
    const sa = String(a.file.frontmatter["_status"] ?? "");
    const sb = String(b.file.frontmatter["_status"] ?? "");
    return sa !== sb ? sa.localeCompare(sb) : a.file.name.localeCompare(b.file.name);
  });
dv.table(["Type", "_Status", "Status", "Entry"],
  pages.map(p => [p.type, p.file.frontmatter["_status"], p.status, p.file.link]));
```

---

## Entries with Open TODOs

```dataviewjs
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => {
    const todo = p.file.frontmatter["_todo"];
    return Array.isArray(todo) && todo.length > 0 && !p.file.frontmatter["_author_only"];
  })]
  .sort((a, b) => a.file.name.localeCompare(b.file.name));
dv.table(["TODOs", "_Status", "Entry"],
  pages.map(p => [p.file.frontmatter["_todo"], p.file.frontmatter["_status"], p.file.link]));
```

---

## Missing Required Fields

### Missing `summary`

```dataviewjs
const po = {high: 0, medium: 1, low: 2};
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => (p.summary == null || p.summary === "") && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99));
dv.table(["Type", "_Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```

### Missing `first_revealed.chapter`

```dataviewjs
const po = {high: 0, medium: 1, low: 2};
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => {
    const ch = p.file.frontmatter["first_revealed"]?.chapter;
    return (ch == null || ch === "") && !p.file.frontmatter["_author_only"];
  })]
  .sort((a, b) => (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99));
dv.table(["Type", "_Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```

### Missing `type`

```dataviewjs
const po = {high: 0, medium: 1, low: 2};
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => (p.type == null || p.type === "") && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99));
dv.table(["Type", "_Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```

### Missing `status`

```dataviewjs
const po = {high: 0, medium: 1, low: 2};
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => (p.status == null || p.status === "") && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99));
dv.table(["Type", "_Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```

### Missing `world_date`

```dataviewjs
const po = {high: 0, medium: 1, low: 2};
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => (p.world_date == null || p.world_date === "") && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99));
dv.table(["Type", "_Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```

---

## All Entries (Active)

```dataviewjs
const pages = [...dv.pages('"world-building/wiki/events"')
  .where(p => p.file.frontmatter["_status"] === "active" && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => {
    const ta = String(a.type ?? "");
    const tb = String(b.type ?? "");
    return ta !== tb ? ta.localeCompare(tb) : a.file.name.localeCompare(b.file.name);
  });
dv.table(["Type", "Status", "_Status", "Priority", "Entry"],
  pages.map(p => [p.type, p.status, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```
