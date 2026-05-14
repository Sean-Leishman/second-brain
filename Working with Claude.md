---
title: Working with Claude
created: 2026-05-14
type: reference
visibility: private
summary: How the second-brain vault works with Claude — what Claude touches, what it doesn't, and the session workflow for compounding learnings.
---

# Working with Claude

A plain-language summary of how this vault operates as an LLM Wiki. The binding contract is [[CLAUDE]] (`CLAUDE.md`); the vault mechanics are in [[00 Vault Guide]]. This page is the orientation layer — read it first if you forget how the whole thing fits together.

## The core idea

Three layers, one rule each:

| Layer | Folders | Rule |
|-------|---------|------|
| **Raw** | `01 Fleeting Notes/`, `02 Sources/`, `06 Daily Notes/`, Telegram/pocket captures | Claude **reads only**. Never rewrites. |
| **Wiki** | `05 Base Notes/`, `04 Indexes/` | Claude **maintains** this. User reviews. |
| **Schema** | `CLAUDE.md` | Co-evolved — updated when a workflow keeps failing. |

The point: raw capture stays immutable and trustworthy, the wiki layer is where knowledge **compounds** instead of being regenerated on every question. Claude does the bookkeeping; the user owns judgment, sourcing, and anything in their own voice.

## What Claude updates

- **`05 Base Notes/`** — synthesised knowledge, one idea per note, in the user's voice. Claude extends/refines/proposes; never authors personal or speculative notes from scratch without assent.
- **`04 Indexes/Wiki Index.md`** — content catalog. Updated on every ingest.
- **`04 Indexes/Wiki Map.md`** — domain shape and gaps. Updated by Reindex.
- **`04 Indexes/Wiki Log.md`** — append-only op history (`## [YYYY-MM-DD] <op> | <subject>`).
- **`04 Indexes/Open Questions.md`** — append-only research backlog. Every unanswerable Query lands here.
- **Topic MOCs** in `04 Indexes/` — kept in sync when affected.
- **`04 Indexes/Digests/`** — weekly/monthly observational digests.

## What Claude must NOT touch

- Daily Notes, journal text, fleeting captures — read-only, always.
- No bulk reorganisation without explicit instruction.
- No fabricated citations — every wiki claim traces to a source, a Daily Note, or the user's stated input.
- No silent rewrites — big edits are diffs the user can accept or reject.
- No authoring opinions on the user's behalf — if a question needs Claude to decide what the user thinks/wants, it stops and asks.

## The operations (slash commands)

| Op | Trigger | What it does |
|----|---------|--------------|
| **`/ingest`** | User points at a `02 Sources/` note | Integrates an already-summarised source into Base Notes; updates provenance, Index, MOC, Log; flips source `#Inbox` → `#Done`. |
| **`/collate`** | About to write a Base Note | Read-heavy. Gathers relevant material, clusters it, proposes new/extend/split/merge. **Propose-only — no writes.** |
| **`/draft`** | "You write it" | Claude drafts the full Base Note from collated material, every claim cited. User reviews. |
| **`/query`** | A question against the wiki | Answers with `[[links]]`; offers to file reusable answers back; logs gaps to Open Questions. |
| **`/digest`** | Weekly (Sun) / monthly (1st) | Observational scan of recent Daily Notes + Sources → patterns, anomalies, candidate Base Notes. |
| **`/lint`** | On demand | Health check — contradictions, stale claims, orphans, broken links, missing cross-refs. |
| **`/reindex`** | Monthly-ish | Wiki-wide structural pass — merges, splits, new MOCs, re-tagging, orphan adoption, decaying-confidence flags. Punch list, not a fait accompli. |

`/collate` and `/reindex` are **propose-only** in their first phase. Claude writes only the items the user accepts, one at a time, with diffs.

## Curate vs Draft mode

Every Base Note is authored in one of two modes — the user picks:

- **Curate** (default for personal/reflective topics) — Claude collates and proposes structure; **user writes** in their own voice; Claude polishes, cross-links, indexes.
- **Draft** (default for technical/synthesis-heavy, or "you write it") — Claude drafts the whole note with cited `[[links]]`; user reviews and edits.

Triggers: "draft it" / "write the note" / "go ahead" → Draft. "collate" / "what should I include" / "I'll write it" → Curate. Unclear → ask once.

## Session workflow — how learnings compound

The lifecycle of a piece of knowledge:

1. **Capture (raw)** — articles/videos via Telegram bot, papers/books via template, thoughts via Daily/Fleeting Notes. Claude doesn't touch this step.
2. **Ingest** — user points Claude at a source. Claude discusses takeaways, surfaces contradictions with existing Base Notes, updates the wiki layer, records provenance.
3. **Synthesise** — over time, repeated themes (3+ mentions, or a strong single signal) become Base Notes. Claude *proposes*; it never auto-creates personal notes.
4. **Query** — questions hit the wiki first, raw only as fallback. Reusable answers get offered back as Base Notes. Unanswered questions become research backlog.
5. **Maintain** — `/lint` catches rot, `/digest` surfaces weekly patterns, `/reindex` restructures monthly.
6. **Co-evolve** — when a workflow keeps failing or the user repeats a correction, `CLAUDE.md` itself gets updated (logged in Wiki Log).

**Project bridge:** when Claude works in `07 Projects/`, load-bearing concepts get cross-checked against `05 Base Notes/`. Generalisable learnings are proposed for promotion into the wiki so project work doesn't become a knowledge leak — the project notes themselves stay in `07 Projects/`. See the next section for the per-session mechanics.

## Working with projects

Projects in `07 Projects/<name>/` are operationally siloed but they shouldn't be amnesiac. Each project session should leave a trail Claude can pick up next time without re-deriving context. Three files per project carry that:

| File | Role | Who writes |
|------|------|------------|
| **`Notes.md`** | Living overview — current state, architecture, key decisions. The "where things stand" doc. | Shared. Claude proposes diffs; user owns it. |
| **`LOG.md`** | Append-only session log, **newest first**. One dated entry per working session. | Claude maintains. |
| **`PLAN.md`** | The active plan for in-flight work. Survives context loss so work can resume. Cleared/archived into `LOG.md` when the work ships. | Claude maintains. |

(Existing example to match: [[Obsidian SSH/LOG]] — dated entries, P0/P1/P2 grouping, an `## Open / next` tail.)

### Session-start checklist

Before doing project work, Claude runs this — it's the "orient" step made explicit:

- [ ] Read `Notes.md` — current state, architecture, decisions.
- [ ] Read the top 2–3 `LOG.md` entries — what recent sessions did and left open.
- [ ] Read `PLAN.md` if it exists — is there in-flight work to resume?
- [ ] Check `## Open / next` in the latest `LOG.md` entry — that's the intended starting point.
- [ ] Cross-check load-bearing concepts against `05 Base Notes/` — link what exists, note what should.
- [ ] Confirm the session's goal with the user if `PLAN.md` and the user's ask disagree.

### Session workflow for projects

1. **Orient** — run the session-start checklist above. That's the working context; don't re-derive it.
2. **Plan** — for anything non-trivial, write the plan to `PLAN.md` *before* executing: goal, steps, files touched, open decisions. If the user approves a plan in-session, it lands here so a later session (or a context reset) can resume it.
3. **Execute** — do the work. Keep `PLAN.md` ticking — check off steps, note deviations.
4. **Log** — at the end of the session (or a meaningful chunk), prepend a dated entry to `LOG.md`:
   - `## [YYYY-MM-DD] — <session title>`
   - **What changed** — concrete deltas, grouped by priority/area if large.
   - **Decisions** — choices made and *why* (the reasoning is the valuable part).
   - **Learnings / insights** — see below.
   - **Open / next** — what's unfinished, what's blocked, what the next session should pick up.
5. **Sync `Notes.md`** — if the session changed the project's overall state or architecture, propose a diff to `Notes.md`. `LOG.md` is the history; `Notes.md` is the current truth.
6. **Promote** — generalisable learnings get flagged for the wiki (see below). When `PLAN.md` work is fully shipped, fold its outcome into the latest `LOG.md` entry and clear the file.

### Plans, summaries, and learnings

- **Saved plans** live in `PLAN.md` — never only in chat. A plan that exists only in conversation is lost on context reset. If a plan is large or multi-phase, keep phase checkboxes in `PLAN.md` so progress is visible across sessions.
- **Session summaries** are the `LOG.md` entry itself — that *is* the summary. Write it for a reader who wasn't there: enough that next session's orientation step is just "read the log."
- **Learnings** split two ways:
  - **Project-specific** (a gotcha in this codebase, a config quirk, a failure mode) → stays in `LOG.md`, or graduates to `Notes.md` / a project `Failure Modes.md` if it's load-bearing. (See [[Beacon/Failure Modes]] for the pattern.)
  - **Generalisable** — an interesting technique, a reusable approach, a non-obvious insight, *an interesting way a task got solved* — → flagged for promotion to a `05 Base Notes/` page via the Project Bridge. Claude **proposes**, doesn't auto-create — projects invent throwaway terminology that shouldn't pollute the permanent layer. During `/reindex`, terms repeated across 2+ projects with no Base Note are strong promotion candidates.
- The test for "is this a wiki learning or a project log entry": *would this help on a different project?* If yes, propose it upward. If it's only true inside this repo, it stays in the project.

### Decision records

Most decisions live fine as a `**Decisions**` line in a `LOG.md` entry. But a decision that is **load-bearing** — it shapes the architecture, it'll be questioned later, reversing it is expensive — gets promoted to a lightweight decision record so the *why* doesn't get buried in chronological log scroll.

- **Where:** a `## Decisions` section in `Notes.md`, or a dedicated `DECISIONS.md` if a project accumulates many. Newest first.
- **Format** (ADR-lite): `### [YYYY-MM-DD] <decision title>` → **Context** (what forced the choice) → **Decision** (what was chosen) → **Why** (alternatives rejected and the reason) → **Status** (`accepted` / `superseded by …`).
- **When Claude writes one:** propose it at log-time when a session's `**Decisions**` line is clearly load-bearing — don't silently inline a major architectural call and move on. The user confirms.
- **Superseding, not deleting:** when a later decision overturns an earlier one, mark the old record `superseded by [[…]]` rather than removing it. The reversal history is itself valuable.
- **Wiki link:** if a decision rests on a concept with a Base Note, cite it. If it *establishes* a generalisable principle, that's a promotion candidate.

### How projects and the wiki interop

The project layer and the wiki layer are separate, but knowledge flows both ways:

- **Project → wiki (promotion).** Generalisable learnings, recurring concepts, and reusable techniques get proposed as Base Notes. When one is promoted, its `sources:` frontmatter cites the originating `LOG.md` entry (or `Notes.md`) — same provenance discipline as `/ingest`, so a Base Note born in a project is still traceable.
- **Wiki → project (reference).** When project work leans on a concept that already has a Base Note, the project note `[[links]]` to it instead of re-explaining. `Notes.md` should accumulate `[[wikilinks]]` to the Base Notes it depends on — that's the project staying anchored to the permanent layer.
- **Project unknowns → Open Questions.** When project work hits something the wiki can't answer (a design question, a "we should research X"), it goes in `04 Indexes/Open Questions.md` with the project as context — the same backlog `/query` feeds. Project research isn't a separate todo silo.
- **Project logs → digests.** Weekly/monthly `/digest` can scan recent project `LOG.md` entries alongside Daily Notes and Sources — surfacing cross-project patterns, repeated friction, and promotion candidates that no single session would notice.
- **Two different "logs" — don't confuse them.** `04 Indexes/Wiki Log.md` records *wiki ops* (ingest/query/lint/reindex/digest) across the whole vault. A project's `LOG.md` records *session work* inside one project. A promotion event touches both: the work is logged in the project `LOG.md`, the new Base Note is logged in `Wiki Log.md`.
- **`/reindex` is the bridge's enforcement pass.** It scans `07 Projects/*/Notes.md` for terms repeated across 2+ projects with no Base Note and flags them. It's the safety net for learnings that should have been promoted in-session but weren't.

### Meta-learnings — working with Claude itself

A distinct, interesting category: not "what we learned about the codebase" but "what we learned about *how to work*" — an approach that worked unusually well, a prompt pattern, a non-obvious way Claude solved a task, a workflow that kept failing.

- Capture these in the `LOG.md` **Learnings** section like any other learning.
- If a pattern recurs across projects, it's a candidate for either a `05 Base Notes/` page (e.g. an "Effective Claude Patterns" note) **or** a `CLAUDE.md` co-evolution edit — the latter when it's a *rule Claude should always follow*, the former when it's *knowledge worth keeping*.
- The dividing line: a meta-learning that should change Claude's default behaviour → `CLAUDE.md` (and log the change in `Wiki Log.md`). A meta-learning that's just useful to remember → Base Note. Repeated corrections of the same behaviour are the strongest signal for a `CLAUDE.md` edit.

## Personal tracking

A sub-domain of the wiki, not a separate vault. Personal facts (sleep baseline, how I learn, recurring patterns) live as flat Base Notes in `05 Base Notes/`, tagged `personal`, `visibility: private`, with a `confidence: high|medium|decaying` field. Curate mode is the default. **Trust rule:** if a recalled personal fact contradicts the user's current statement, trust the current statement and update the fact — personal facts decay. Decaying notes (no reinforcing signal in 8+ weeks) get flagged in digests/reindex for refresh or retirement.

## Conventions cheat-sheet

- Frontmatter on every wiki page: `created`, `tags`, `visibility`, `summary`, `links`.
- Base Notes carry `sources: [[...]]` provenance — maintained by `/ingest`, enables traceback when a source is challenged.
- Wikilinks `[[Note Name]]`, not paths (except inside `02 Sources/`).
- ISO dates `YYYY-MM-DD`.
- Voice: Base Notes = user's synthesis voice. Source notes = reportorial. Digests = observational ("this week showed X").

## See also

- [[CLAUDE]] — the full contract
- [[00 Vault Guide]] — vault structure, folders, capture pipeline
- [[Wiki Index]] · [[Wiki Map]] · [[Wiki Log]] · [[Open Questions]]
