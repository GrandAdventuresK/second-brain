# sources/

External inputs — things you didn't write. Books, articles, papers, podcasts, talks, videos, courses.

A source note records *what they said* and *what you flagged*. Your own thinking about it belongs in [`../notes/`](../notes/) or a learning topic's synthesis, linked back to the source.

## Required frontmatter

Every source note starts with YAML frontmatter so the vault is queryable by AI and by you. Empty optional fields are fine; required fields must be filled.

```yaml
---
title: "Article or book title"
authors: ["Last, First", "Last, First"]
year: 2026
type: article          # article | book | chapter | paper | podcast | talk | video | course | post
venue: "Leadership Quarterly"   # journal / publisher / podcast — optional
link: "https://..."             # canonical URL or DOI
captured: 2026-05-24
status: skimmed                  # skimmed | read | studied | re-read
paths: [leadership-and-identity] # which learning paths this feeds
topics: []                       # cross-cutting topic tags (match topics/ filenames)
schools: []                      # for leadership: developmental | adaptive | authentic | etc.
key_claim: "One sentence — the main argument."
relevance: "Why I care, in one line."
canonical: false                 # is this a canonical-for-the-field source?
paywalled: false
source_cost: "free via library"  # free | $X | "library e-lending" | "open access"
---
```

**Required:** `title`, `type`, `link`, `captured`, `paths`, `key_claim`.
**Optional but encouraged:** everything else.

## Body shape after the frontmatter

No mandatory template. A useful starting shape:

```
# Title

## Highlights

> Quote 1

> Quote 2

## My take

(your thoughts — or link out to a separate note if it's substantial)
```

## Naming

- `kebab-case.md`, often prefixed with the type: `book-thinking-in-systems.md`, `article-some-piece.md`.
- Or just the title: `thinking-in-systems.md`. Whichever stays out of your way.
