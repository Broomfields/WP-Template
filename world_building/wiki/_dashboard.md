---
title: "Wiki Master Dashboard"
_author_only: true
---

# Wiki Master Dashboard

> Author-only. Not pushed to the CMS.

---

## Entry Counts by Category

```dataviewjs
const pages = dv.pages('"world_building/wiki"')
  .where(p => !p.file.frontmatter["_author_only"] && p.entity != null);
const groups = {};
for (const p of pages) {
  const key = String(p.entity);
  groups[key] = (groups[key] ?? 0) + 1;
}
dv.table(["Entity", "Total Entries"],
  Object.entries(groups).sort(([a],[b]) => a.localeCompare(b)));
```

---

## Overall Draft vs Active Breakdown

```dataviewjs
const pages = dv.pages('"world_building/wiki"')
  .where(p => !p.file.frontmatter["_author_only"] && p.entity != null);
const groups = {};
for (const p of pages) {
  const key = String(p.file.frontmatter["_status"] ?? "(none)");
  groups[key] = (groups[key] ?? 0) + 1;
}
dv.table(["_Status", "Count"],
  Object.entries(groups).sort(([a],[b]) => a.localeCompare(b)));
```

---

## All Entries Flagged for Review

```dataviewjs
const pages = [...dv.pages('"world_building/wiki"')
  .where(p => p.file.frontmatter["_review_needed"] === true && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => {
    const ea = String(a.entity ?? "");
    const eb = String(b.entity ?? "");
    if (ea !== eb) return ea.localeCompare(eb);
    const po = {high: 0, medium: 1, low: 2};
    return (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99);
  });
dv.table(["Entity", "Type", "_Status", "Priority", "Entry"],
  pages.map(p => [p.entity, p.type, p.file.frontmatter["_status"], p.file.frontmatter["_priority"], p.file.link]));
```

---

## All High-Priority Entries

```dataviewjs
const pages = [...dv.pages('"world_building/wiki"')
  .where(p => p.file.frontmatter["_priority"] === "high" && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => String(a.entity ?? "").localeCompare(String(b.entity ?? "")));
dv.table(["Entity", "Type", "_Status", "Entry"],
  pages.map(p => [p.entity, p.type, p.file.frontmatter["_status"], p.file.link]));
```

---

## All Draft Entries

```dataviewjs
const pages = [...dv.pages('"world_building/wiki"')
  .where(p => p.file.frontmatter["_status"] === "draft" && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => {
    const ea = String(a.entity ?? "");
    const eb = String(b.entity ?? "");
    if (ea !== eb) return ea.localeCompare(eb);
    const po = {high: 0, medium: 1, low: 2};
    return (po[a.file.frontmatter["_priority"]] ?? 99) - (po[b.file.frontmatter["_priority"]] ?? 99);
  });
dv.table(["Entity", "Type", "Priority", "Entry"],
  pages.map(p => [p.entity, p.type, p.file.frontmatter["_priority"], p.file.link]));
```

---

## Entries Missing Required Fields

### Missing `summary`

```dataviewjs
const pages = [...dv.pages('"world_building/wiki"')
  .where(p => (p.summary == null || p.summary === "") && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => String(a.entity ?? "").localeCompare(String(b.entity ?? "")));
dv.table(["Entity", "Type", "_Status", "Entry"],
  pages.map(p => [p.entity, p.type, p.file.frontmatter["_status"], p.file.link]));
```

### Missing `first_revealed.chapter`

```dataviewjs
const pages = [...dv.pages('"world_building/wiki"')
  .where(p => {
    const ch = p.file.frontmatter["first_revealed"]?.chapter;
    return (ch == null || ch === "") && !p.file.frontmatter["_author_only"];
  })]
  .sort((a, b) => String(a.entity ?? "").localeCompare(String(b.entity ?? "")));
dv.table(["Entity", "Type", "_Status", "Entry"],
  pages.map(p => [p.entity, p.type, p.file.frontmatter["_status"], p.file.link]));
```

### Missing `type`

```dataviewjs
const pages = [...dv.pages('"world_building/wiki"')
  .where(p => (p.type == null || p.type === "") && !p.file.frontmatter["_author_only"])]
  .sort((a, b) => String(a.entity ?? "").localeCompare(String(b.entity ?? "")));
dv.table(["Entity", "_Status", "Entry"],
  pages.map(p => [p.entity, p.file.frontmatter["_status"], p.file.link]));
```

---

## Entries with Open TODOs

```dataviewjs
const pages = [...dv.pages('"world_building/wiki"')
  .where(p => {
    const todo = p.file.frontmatter["_todo"];
    return Array.isArray(todo) && todo.length > 0 && !p.file.frontmatter["_author_only"];
  })]
  .sort((a, b) => String(a.entity ?? "").localeCompare(String(b.entity ?? "")));
dv.table(["Entity", "TODOs", "Entry"],
  pages.map(p => [p.entity, p.file.frontmatter["_todo"], p.file.link]));
```
