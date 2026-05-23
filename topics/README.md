# topics/

Wiki-style topic pages. The connective layer of the vault.

Each file in this folder is "everything I know and think about X, with links to the notes that back it up." Paragraphs of your own synthesis, interrupted with `[[links]]` to atomic notes, sources, and learning notebooks.

## What a topic page looks like

No rigid template. A good topic page reads like a short essay you'd send a friend asking "what do you know about X?" Loose structure, dense with links.

Example:

```
# Systems Thinking

Systems thinking is the discipline of seeing wholes, not parts.
I keep coming back to [[feedback-loops]] as the engine of dynamic behavior,
and [[stocks-and-flows]] as the basic vocabulary.

## Key ideas

- [[feedback-loops]] — positive and negative loops
- [[stocks-and-flows]] — what accumulates, what passes through
- [[leverage-points]] — where to intervene in a system

## Sources I've drawn from

- [[book-thinking-in-systems-meadows]]
- [[article-some-piece]]

## Open questions

- How does this relate to [[ecosystem-design]]?
```

## How topic pages stay current

Don't try to maintain these by hand. Use the `tend-topics` skill — it scans new notes, finds orphans, and proposes additions. See [`../.claude/skills/tend-topics/SKILL.md`](../.claude/skills/tend-topics/SKILL.md).

Invoke it with: **"Run tend-topics"** after a study session, weekly review, or whenever `inbox/` feels heavy.

## What's NOT a topic page

- Not a learning curriculum — that's [`../learning/<topic>/path.md`](../learning/).
- Not an area of responsibility — that's [`../areas/`](../areas/).
- Not a project plan — that's [`../projects/`](../projects/).

A topic page is *connection*, not action or commitment.
