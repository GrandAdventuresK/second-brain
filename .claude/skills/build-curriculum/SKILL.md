---
name: build-curriculum
description: Design rigorous college-level curricula for any learning path in the vault. Operates at three nested levels — program, semester, course — triangulating real university programs and curating from freely available sources first, flagging paid canonical texts as "[buy if essential]". Interactive — asks design questions until it has enough to generate something calibrated, never one-shot defaults. Use when the user says "build curriculum", "design the program", "plan semester N", "build a course on X", or invokes `/build-curriculum [program|semester|course] <path> [<arg>]`.
---

# Build Curriculum

This skill designs the actual coursework that sits inside a learning path. It's the bridge between the strategic `curriculum.md` (which says "Phase 1 is coursework + literature + methods") and the reading-by-reading work the user actually does.

The skill operates at three nested levels. The user invokes at the level they need. Each level reads what's already in the vault and can run standalone — you don't need `program.md` to exist before building a semester, though if it does, use it.

## Three operations

| Level | Invocation | Produces |
| --- | --- | --- |
| Program | `/build-curriculum program <path>` | `learning/<path>/program.md` |
| Semester | `/build-curriculum semester <path> <N>` | `learning/<path>/semesters/semester-<N>.md` |
| Course | `/build-curriculum course <path> "<course-slug>"` | `learning/<path>/courses/<slug>.md` |

`<path>` is a directory name under `learning/` (e.g. `leadership-and-identity`).

If the user invokes without arguments or with ambiguity (e.g. just "/build-curriculum"), ask which level they want.

## General principles, all levels

### Interactive — ask before generating

This skill is conversational. **Do not generate output until you have enough information.** Ask as many questions as needed. Typical sessions involve 4–8 design questions before any file is written. The user explicitly preferred this over one-shot drafts.

Use `AskUserQuestion` for multiple-choice design questions (level, depth, focus emphasis). Ask in plain text for open-ended ones (existing prereqs, specific texts the user wants included).

Err on the side of asking. Do not assume.

### Triangulate from real programs — don't invent

Before generating any structure, read `.claude/skills/build-curriculum/references.md` for the list of reference programs (HBS, Stanford GSB, MIT Sloan, Yale SOM, Penn Wharton, Case Western Weatherhead, etc.) and the free-source preference order. Cite which programs the design draws from in the output's header so the user can verify.

When in doubt, use `WebSearch` and `WebFetch` to pull current syllabi from named programs and incorporate. Never invent a university or a program. If you can't find a syllabus, say so.

### Substitute + flag for paid sources

The user does not have a textbook budget. For every required reading:

1. Prefer freely available sources (see `references.md` for the preference order).
2. When the canonical work is paid-only, substitute the best free analog (HBR article summarizing the book, author's YouTube lecture covering the same ground, preprint of a chapter, OCW lecture series) as the **primary** requirement.
3. Flag the original as `[buy if essential: ~$N]` with rough cost so the user can decide later.
4. **Never silently skip a canonical work** — always name it and explain the substitution.

### Default to doctorate-level depth

Doctorate-level means: primary sources not summaries; engagement with debates and gaps; critical reading; original synthesis expected. Master's-level means: synthesis of the literature; ability to apply frameworks; quality essays.

If the user hasn't specified, ask. Default assumption (for the leadership-and-identity major) is doctorate.

### Realistic load

Doctorate-level coursework should be ~10–15 hrs/week realistic for a working founder, not 40. If the design implies more than that, flag it and offer to thin.

## Operation: program

Produces `learning/<path>/program.md` — the full structure for the path.

### Questions to ask first (minimum)

1. **Level:** master's, doctorate, or hybrid?
2. **Reference programs to weight more heavily:** any preferences? (e.g., "lean toward HBS-style case method" or "lean toward developmental-psychology programs like Case Western Weatherhead")
3. **Existing prereqs the user satisfies:** undergrad business? prior management experience? prior coursework? (Determines what to skip.)
4. **Focus emphasis within the field:** for leadership: developmental? adaptive? founder-specific? authentic? balanced across?
5. **Courses per semester:** typical doctorate is 2–3; master's is 3–4. User may differ.
6. **Total intended semesters** OR "open-ended" — design assumes 6–8 semesters for doctorate, 3–4 for master's.
7. **Known gaps the user wants the program to address.**

Ask follow-ups as needed. Don't move to generation until the design is clear.

### Output structure (`program.md`)

1. **Header** — level, reference programs triangulated (list them), intended duration, courses per semester.
2. **Prerequisites** — what should be done first, with notes on whether the user satisfies each.
3. **Required core courses** — numbered list, each with: title, one-line description, prereqs, target semester.
4. **Methods sequence** — methods courses in order (doctorate-essential).
5. **Specialization / electives** — options the user picks from in later semesters.
6. **Capstone** — description: thesis / dissertation / framework / book.
7. **Comprehensive exam** — when, format, scope.
8. **Semester-by-semester plan** — table showing course load per semester.
9. **Source-freedom note** — rough estimate of % of canonical reading freely available; named flagged-paid texts.
10. **Forcing function integration** — when teach-to-team / GA interventions / comp papers happen across the program.

## Operation: semester

Produces `learning/<path>/semesters/semester-<N>.md`. May run with or without `program.md` existing. If `program.md` exists, use it for context. If it doesn't, ask the user enough to build a coherent semester anyway.

### Questions to ask first (minimum)

1. **Which semester (N)** — confirm.
2. **If no `program.md`:** brief program context — level, focus emphasis, what prior semesters covered.
3. **Time available this semester** — full load, half-load, lighter?
4. **Course overrides** — any courses the user wants to swap in/out from what's expected?
5. **Specific learning gaps** to address this semester?
6. **Length in weeks** — typical 12–15, semester or trimester?

### Output structure (`semesters/semester-<N>.md`)

1. **Header** — semester N, courses, total weekly hours estimated, length.
2. **Courses this semester** — each: title, target hours/week, prereqs satisfied, sub-folder reference (if course doc exists).
3. **Sequence within semester** — which to start first, which run in parallel.
4. **Semester deliverable** — the comp paper this semester drives toward.
5. **Forcing functions** — teach-to-team scheduled, GA intervention(s), prediction commitments.
6. **Weekly view** — a table showing weeks 1 through N, what's happening in each course each week.
7. **Reading volume estimate** — total pages/hours of reading per week, so the load is honest.

## Operation: course

Produces `learning/<path>/courses/<slug>.md`. May run standalone — sometimes the user wants to build a single course without a full program.

### Questions to ask first (minimum)

1. **Course title and brief topic** if not obvious from the slug.
2. **Depth target:** master's (~3–4 hrs/week) or doctorate (~6–10 hrs/week)?
3. **Length in weeks** (typical 12–15).
4. **Focus emphasis** within the course topic.
5. **Specific texts / authors / papers** the user wants included.
6. **Assessment format:** paper, project, build, teach-to-team, oral defense, exam — possibly multiple.
7. **Methods or lab component** to integrate?

### Output structure (`courses/<slug>.md`)

1. **Header** — title, level, depth, length, prereqs assumed.
2. **Course description** — 1–2 paragraphs.
3. **Learning objectives** — 3–5, written as "by the end you will be able to ___."
4. **Reference programs / syllabi consulted** — list with links where public.
5. **Schedule** — week-by-week:
   - Week N: topic
   - Required readings (with URLs for free, `[buy if essential: ~$N]` for paid)
   - Optional readings
   - Discussion / synthesis questions (3–5)
   - Practice activity (if applicable)
6. **Methods/lab work** if integrated.
7. **Assessment** — format, rubric.
8. **Teach-to-team deliverable** — what the user will turn into a 30-min internal talk at the end.
9. **Source freedom audit** — count of free vs. flagged-paid vs. library-hold readings; cost if the user buys everything flagged.

## After generating, at any level

1. Show the user the full draft inline before writing the file.
2. Offer 2–3 specific revision angles ("want me to lean heavier on developmental psych?", "want to shorten the weekly load?", "swap the Edmondson reading for the Detert one?").
3. Write the file once the user approves.
4. If the user is on a working branch, offer to commit and push (don't do it silently).

## What NOT to do

- **Don't generate without asking design questions first.** Even if the invocation looks obvious, ask the minimum questions for that level.
- **Don't invent universities, programs, or syllabi.** Only cite real ones. Use `WebSearch`/`WebFetch` to verify if uncertain.
- **Don't fabricate URLs.** If a reading exists online and you can find it, link it. Otherwise note "find via Google Scholar" or "library hold."
- **Don't silently skip canonical work because it's paid** — always name it and substitute or flag.
- **Don't overwrite existing program.md / semester / course files** without asking first.
- **Don't make the curriculum unrealistic.** Doctorate-level coursework should be ~10–15 hrs/week for a working founder. If a design implies 40+, flag and offer to thin.
- **Don't conflate this skill with the daily block ritual.** This skill *designs* the curriculum; `block-ritual.md` is the daily practice run *inside* the curriculum.
- **Don't pad with filler.** If a week genuinely has only 2 readings worth doing, list 2. Don't invent a third for symmetry.

## When to invoke

User says any of:

- "build curriculum", "build the curriculum", "design the program"
- "/build-curriculum ..." in any form
- "let's design semester N", "plan semester N"
- "build the course for X", "design a course on Y", "what should a course on Z look like"
- "what would a master's/doctorate in X consist of"

Do NOT invoke proactively. Always wait for the user to explicitly ask.
