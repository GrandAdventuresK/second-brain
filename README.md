# Second Brain

A growing system for learning, thinking, and keeping up.

Built organically — every folder, every convention here exists because it earned its place. Nothing was added "just in case." When something stops earning its keep, it gets removed.

## Philosophy

- **Folders express *where in the lifecycle* something is** — capture, input, thinking, study, synthesis, responsibility, delivery.
- **Links express *what something is about*** — `[[wiki-links]]` between notes do the work folders can't, because a single idea can belong to many topics.
- **Topic pages do the connective work** — see [`topics/`](topics/) — but they're maintained as a periodic ritual, not a constant tax.
- **Capture without classifying.** When in doubt, drop it in [`inbox/`](inbox/). Sorting can wait.

## The seven folders

| Folder | What lives here | Lifecycle stage |
| --- | --- | --- |
| [`inbox/`](inbox/) | Raw, unsorted capture | Newly arrived |
| [`sources/`](sources/) | External inputs — articles, books, talks, podcasts | Borrowed |
| [`notes/`](notes/) | Atomic notes in *your* words; cross-cutting ideas | Your own |
| [`learning/`](learning/) | Structured topical study — path, synthesis, practice, learning-projects | Active study |
| [`topics/`](topics/) | Wiki-style topic pages that connect everything | Curated synthesis |
| [`areas/`](areas/) | Ongoing responsibilities you maintain | Standing |
| [`projects/`](projects/) | Active deliverables with outcomes and deadlines | Shipping |

## Lifecycle of a thought

```
inbox ─┬─► sources  ─►  notes  ─┐
       │                        ├─► topics
       ├─► learning/<topic>/  ──┘
       │      synthesis
       │
       └─► areas / projects
```

You capture freely in `inbox/`. You read or watch something — that's a `source`. You write your own thoughts about it — that's a `note` (or, if it's part of a structured study, it goes into a `learning/<topic>/synthesis/`). Periodically, the `tend-topics` skill helps stitch atomic notes into `topics/` pages so connection compounds over time.

## The learning spine *(if you're using this vault for structured study)*

Four documents at the root anchor a self-designed program of study:

- [`through-line.md`](through-line.md) — the unifying question the whole vault is in service of. Evolves.
- [`curriculum.md`](curriculum.md) — strategic architecture: major + contributing disciplines, phases, methods, validation.
- [`validation.md`](validation.md) — the predict-before-act and falsifiable-claim disciplines that make markets and readers actually bite.
- [`block-ritual.md`](block-ritual.md) — the operational practice. Every learning block runs this loop.

These four sit *above* the folders — they tell you what the folders are *for*.

## Conventions

- **Filenames:** `kebab-case.md` (e.g., `feedback-loops.md`). Easy to link, easy to type, no escaping needed.
- **Wiki-links:** `[[note-name]]` — works in Obsidian, Logseq, and most modern markdown editors.
- **Frontmatter:** optional. Use when useful. Don't impose ceremony on yourself.

## The `tend-topics` ritual

Topic pages don't maintain themselves. The `tend-topics` skill is how we keep them current without it becoming a burden.

When you've added new notes (after a study session, during a weekly review, whenever `inbox/` feels heavy), ask:

> "Run tend-topics"

It scans your recent notes, finds orphans (notes not yet linked from any topic), surfaces stale topic pages, and proposes new topics for emerging clusters. You approve; it applies. See [`.claude/skills/tend-topics/SKILL.md`](.claude/skills/tend-topics/SKILL.md).

## Tools that play well with this vault

- [Obsidian](https://obsidian.md) — graph view, wiki-links, mobile capture
- [Logseq](https://logseq.com) — outliner-style, also markdown-native
- VS Code with the Foam or Markdown All in One extensions
- `git grep` and your text editor

## What's deliberately *not* here (yet)

- No `archive/`. Archive when archiving earns its keep.
- No rigid templates. Add them when you find yourself rewriting the same opening twice.
- No tags taxonomy. Use tags ad-hoc; if a pattern emerges, document it.
