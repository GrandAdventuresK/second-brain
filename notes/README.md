# notes/

Atomic notes in your own words.

One idea per note. The note should be useful out of context — if you stripped all the links, would the idea still hold? An atomic note is the smallest reusable unit of your thinking.

## Required frontmatter

Every note starts with YAML frontmatter so the vault is queryable by AI and by you.

```yaml
---
title: "The idea, stated as a phrase"
created: 2026-05-24
updated: 2026-05-24
type: atomic                   # atomic | synthesis | claim | question | observation
paths: []                       # which learning paths this connects to
topics: []                      # cross-cutting topic tags (match topics/ filenames)
sources: []                     # source notes this rests on (filenames without .md)
related: []                    # other notes
status: seed                    # seed | developing | mature
---
```

**Required:** `title`, `created`, `type`, `status`.
**Optional but encouraged:** everything else.

`updated` should be bumped whenever you meaningfully revise the note.

## When to write here vs. in `learning/<topic>/synthesis/`

- **Cross-cutting idea** that touches multiple topics → here.
- **Born inside a structured study** → start in `learning/<topic>/synthesis/`, promote here once it proves cross-cutting.
- **Stray insight** with no clear topical home → here.

## Naming

- `kebab-case.md` — `feedback-loops.md`, `slack-is-a-feature.md`.
- The title is the idea, not a category.

## Linking

Use `[[wiki-links]]` liberally. Atomic notes get their power from interconnection. Don't link out of obligation — link when you'd actually want to follow the thread.
