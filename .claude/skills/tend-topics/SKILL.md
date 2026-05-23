---
name: tend-topics
description: Maintain topic pages in topics/ by scanning notes/, learning/*/synthesis/, and recent inbox/ items. Surfaces orphan notes, stale topics, and emerging topic clusters, then applies edits the user approves. Use when the user asks to "tend topics", "update topics", "refresh maps", "run tend-topics", or after they've added several notes and want their topic layer brought current.
---

# Tend Topics

This skill is the maintenance ritual for the second brain's topic layer. It keeps `topics/*.md` (wiki-style topic pages) in sync with atomic notes scattered across `notes/`, `learning/*/synthesis/`, and recent `inbox/` items.

The user explicitly said they get lost in LYT/MOC workflows. Your job is to carry the indexing burden for them, propose edits clearly, and only apply changes they approve.

## What to do

### 1. Inventory

List all markdown files in:
- `notes/**/*.md`
- `learning/*/synthesis/**/*.md`
- `inbox/**/*.md` — filter to items older than 24h based on file mtime, to give the user time to process them
- `topics/*.md`

Exclude any `README.md` files from the inventory of "atomic notes" — those are folder docs, not content.

### 2. Build a link map

For each atomic note, find which topic pages already link to it. Detection rules:
- A topic page links to a note if it contains `[[note-name]]` or `[text](relative/path/to/note.md)` referencing the file.
- Match by filename without extension, case-insensitive.

### 3. Find orphans

Atomic notes not linked from any topic page. For each orphan:
- Propose 0–3 topic pages it could fit into, based on filename keywords, headings, and content.
- Provide a one-line rationale per proposal.
- If no existing topic fits, flag the note as a candidate for a new topic.

### 4. Find stale topics

Topic pages whose linked atomic notes have a more recent `mtime` than the topic page itself. Surface them with:
- Topic name
- Notes that have been modified since the topic was last touched
- Suggested edits (additions, reorganizations) — keep these as suggestions, not assertions.

### 5. Find emerging topics

Clusters of 3+ related orphan notes. Detect relatedness by:
- Shared tags (if frontmatter tags exist)
- Common keywords in titles or headings
- Cross-references between the orphan notes themselves

For each emerging cluster, draft a new topic page with:
- A working title
- 2–3 paragraphs of synthesis stitching the notes together (paraphrase from actual note contents)
- A "Notes" section linking to each member of the cluster

### 6. Present a plan

Before making any edits, show the user three sections:

```
## Orphans (N notes)
- notes/some-note.md → suggest adding to topics/systems-thinking.md
  rationale: mentions feedback loops, references Meadows
- notes/other-note.md → no good fit; candidate for new topic "ecosystem-design"
...

## Stale topics (N topics)
- topics/systems-thinking.md — 3 linked notes modified since last touch
  suggest: add a paragraph on [[leverage-points]] (recently expanded)
...

## Emerging topics (N candidates)
- "ecosystem-design" — draft gathers 4 orphan notes
  (show the draft inline)
...
```

Then ask the user which subset to apply. Default to applying nothing without explicit approval.

### 7. Apply on approval

Once the user approves any subset:
- **Orphan → topic additions:** edit the target topic page, adding a `[[link]]` in an appropriate section. If no section fits, add to a "More notes" catch-all at the bottom.
- **Stale topic updates:** apply the specific edits the user approved.
- **New topics:** create the new file in `topics/`.

After applying, show a brief summary of what changed.

## Tone and style of topic pages

Topic pages are NOT rigid templates. They are written like a short essay or wiki article: the user's own synthesis in paragraphs, interrupted with `[[wiki-links]]`. Mimic existing topic pages in the vault. If none exist yet, use loose paragraphs + a "Notes" section of linked atomic notes. See `topics/README.md` for the example shape.

When drafting new topic pages or synthesis paragraphs, write in the user's voice as much as you can infer from existing notes. **Do not invent claims they haven't made — paraphrase from their actual notes.**

## What NOT to do

- Don't move or rename files. The user owns file organization.
- Don't edit atomic notes themselves. Only edit topic pages.
- Don't create a topic page for fewer than 3 related notes.
- Don't auto-process inbox items — only surface them as context for topic updates.
- Don't apply edits without showing a plan and getting approval.
- Don't impose templates or formatting beyond what already exists in the vault.
- If a note's topical home is ambiguous, ask. Don't guess silently.

## When to invoke

The user invokes this skill when:
- They explicitly ask ("tend topics", "update topics", "refresh maps", "run tend-topics")
- After a study session, when they've added several synthesis notes
- During a weekly/periodic review
- When `inbox/` feels heavy and they want help processing

Do NOT proactively invoke this skill outside those moments.
