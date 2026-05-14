---
title: CLAUDE.md
created: 2026-05-06
type: schema
visibility: private
---

# Vault Schema (LLM Wiki)

This file defines how an LLM agent operates inside this Obsidian vault. It is the schema layer in the [Karpathy LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — raw sources stay immutable, the wiki layer is agent-maintained, and this file is the contract.

For *vault structure, folder purposes, Zettelkasten pipeline, and capture workflows*, the source of truth is [[00 Vault Guide]]. Read it first. This file only adds the agent-maintainer layer on top.

---

## Roles

**User owns:** sourcing, exploration, asking questions, judgment, ground truth about themselves, decisions about priorities. Daily Notes, journal entries, fleeting captures, and anything authored in the user's voice are inviolable — never rewrite them.

**Agent owns:** bookkeeping. Summaries, cross-references, MOC maintenance, contradiction flagging, digest drafting, lint passes, log entries. The agent should compound knowledge into the wiki layer, not regenerate it on every query.

**Shared (Base Notes):** Either the user or the agent can draft a Base Note. Two explicit modes — the user picks which one applies per session or per note:

- **Curate mode** (default for personal/reflective topics) — agent runs *Collate* and proposes structure, user writes the note in their own voice. Agent polishes, cross-links, indexes.
- **Draft mode** (default for technical/synthesis-heavy topics, or when user says "you write it") — agent drafts the full Base Note from collated material. User reviews and edits. Agent's draft must cite sources with `[[links]]` for every claim.

When the user says "draft it" / "write the note" / "go ahead" → Draft mode. When they say "collate" / "what should I include" / "I'll write it" → Curate mode. When unclear, ask once: *"Draft or curate?"*

In either mode: the user's authored content stays in their voice; agent edits are diffs the user can accept or reject. Personal facts about the user default to Curate mode unless explicitly told otherwise — the user's self-portrait should be in their own words.

If a question would require the agent to *decide what the user thinks/wants/believes*, stop and ask. The agent does not author opinions on the user's behalf.

---

## Three Layers (mapped to this vault)

| Layer | Folder(s) | Who writes |
|-------|-----------|------------|
| **Raw (immutable to agent)** | `01 Fleeting Notes/`, `02 Sources/`, `06 Daily Notes/`, pocket-jot/Telegram captures | User (or capture pipeline). Agent reads only. |
| **Wiki (agent-maintained)** | `05 Base Notes/`, `04 Indexes/` | Agent writes; user reviews and corrects. |
| **Schema** | This file (`CLAUDE.md`) | Co-evolved. |

Treat `02 Sources/` as raw *input* but **summary/synthesis pages inside source notes are agent-writable** when the user explicitly asks for ingest. The literature notes themselves are agent-drafted, user-approved.

`07 Projects/` is project-scoped and follows its own conventions (see Vault Guide). The agent may help with `Notes.md`/`Todo.md` but does not unilaterally rewrite them.

`08 Trackers/` are user-owned operationally; agent may suggest moves between Inbox/This Week/Someday but waits for confirmation before bulk-editing.

---

## Wiki Navigation Files

Four files in `04 Indexes/` serve as the agent's navigation surface:

- **`04 Indexes/Wiki Index.md`** — content catalog. Agent updates on every ingest. Sections by category: *Concepts*, *Personal*, *People*, *Sources by topic*. Each entry: link + one-line summary.
- **`04 Indexes/Wiki Map.md`** — top-level map of MOCs. Hand-curated overview of *which domains exist in the wiki*, density per domain, gaps. Updated by **Reindex** op. The Index lists every page; the Map shows shape.
- **`04 Indexes/Wiki Log.md`** — append-only chronological record. Format: `## [YYYY-MM-DD] <op> | <subject>` so it's greppable. Ops: `ingest`, `query`, `lint`, `reindex`, `digest`.
- **`04 Indexes/Open Questions.md`** — append-only research backlog. Every Query that the wiki couldn't fully answer ends here. Each entry: question, date, what was missing (source vs Base Note), suggested next action.

Topic-specific MOCs (existing pattern) continue to live in `04 Indexes/` alongside these.

---

## Operations

### Ingest

**Source-summary generation is already handled** by the Telegram bot (articles/videos) and manual templates (papers/books) — see [[00 Vault Guide]]. The agent does *not* duplicate that step.

Ingest in this schema means **integrating an already-summarised source into the wiki layer**. Triggered when the user points at a source note in `02 Sources/` and says "ingest" (or drops one in via Telegram and asks for follow-through).

1. Read the source note (already-written summary).
2. **Discuss takeaways with the user** if the source is substantive — surface anything that contradicts prior wiki claims, extends an existing Base Note, or warrants a new one.
3. Update relevant Base Notes in `05 Base Notes/` — extend, refine, or propose splits. *Propose new Base Notes; do not create them silently.* See **Collate** for authoring rules.
4. **Maintain provenance:** add the source to the `sources:` frontmatter field of every Base Note that absorbs material from it (see *Conventions → Source provenance*).
5. Update `04 Indexes/Wiki Index.md` and any topic MOC affected.
6. Flip the source note's status from `#Inbox` to `#Done`.
7. Append to `04 Indexes/Wiki Log.md`.

If the user pastes a raw URL/PDF directly to the agent (bypassing the bot), the agent may write the source note itself using the relevant template — but the bot is the preferred path. Default to **single-source ingest with the user in the loop**, not batch.

### Query

User asks a question against the wiki.

1. Read `04 Indexes/Wiki Index.md` first; pick relevant pages from the catalog.
2. Read those pages. If they're insufficient, fall back to grep/search across the wiki layer, then raw if needed.
3. Synthesise with citations as `[[Note Name]]` links.
4. **If the answer is non-trivial and reusable** (a comparison, an analysis, a connection), offer to file it back as a new Base Note or MOC entry. The user decides.
5. If the answer required reading raw sources the wiki had not yet absorbed, flag it — that's a signal those sources need ingestion.
6. **If the wiki could not fully answer**, append the question to `04 Indexes/Open Questions.md` with date, gap (missing source vs missing Base Note vs unresolved contradiction), and suggested next action. This is non-optional — the Question Log is the research backlog.

### Collate

Triggered when the user is drafting (or about to draft) a Base Note, or asks "what should I collate on X?". This is the agent's main job in user-authored synthesis.

1. Search across `01 Fleeting Notes/`, `02 Sources/`, `06 Daily Notes/`, and existing `05 Base Notes/` for material relevant to the topic.
2. Group findings into clusters: *direct evidence*, *adjacent concepts*, *contradictions*, *open threads*.
3. Propose one of: **new Base Note** (with suggested title + skeleton), **extend existing Base Note** (with the specific section to add), **split existing Base Note** (when one note now covers two distinct ideas), or **merge two Base Notes** (when they've drifted into the same concept).
4. Cite every suggestion with `[[links]]` so the user can verify before deciding.
5. If the user accepts and writes the note themselves, agent's job becomes polish + cross-link + Index update. If the user delegates the draft, agent writes; user reviews.

Collate is read-heavy and propose-only by default. No file writes until the user picks a direction.

### Reindex

Wiki-wide structural pass. Triggered on demand (e.g. monthly, or when the wiki feels noisy). Distinct from **Lint** (health check) and **Collate** (single-note focus) — Reindex looks at the whole wiki and proposes reorganisation.

1. **Scan** all `05 Base Notes/` and `04 Indexes/`. Optionally include `02 Sources/` if asked.
2. **Cluster** by topic — group notes that share concepts, citations, or tags. Surface unexpected clusters (notes that should be linked but aren't).
3. **Propose:**
   - **New MOC pages** when a cluster has 3+ Base Notes and no existing index page.
   - **Merge candidates** — pairs of Base Notes that have drifted into covering the same concept. Show overlap and suggest which to keep as canonical.
   - **Split candidates** — single Base Notes that now cover two distinct ideas (length, multiple unrelated sections, divergent inbound links).
   - **Re-tagging** — notes whose tags don't match their actual content, or missing tags.
   - **Index updates** — `04 Indexes/Wiki Index.md` entries to add, remove, or rewrite.
   - **Map updates** — `04 Indexes/Wiki Map.md` regenerated to reflect current domain shape, density, and gaps.
   - **Orphan adoption** — notes with no inbound links that belong in an existing MOC.
   - **Decaying confidence** — personal Base Notes with no reinforcing signal in 8+ weeks flagged for refresh.
   - **Cross-project promotions** — concepts repeated across 2+ projects in `07 Projects/` with no Base Note (see *Project ↔ Wiki Bridge*).
4. **Output a punch list**, not a fait accompli. Each suggestion: *what*, *why*, *which files*, *Curate or Draft mode if action involves authoring*.
5. User picks which to act on. Agent executes only the accepted items, one at a time, with diffs.
6. Append a `reindex` entry to `Wiki Log.md` summarising what was proposed and what was accepted.

**Default cadence:** monthly. **Default scope:** Base Notes + Indexes. Sources only on request — Source Notes are tied to immutable artifacts and shouldn't be reorganised lightly.

Reindex is read-and-propose by default. **No file writes during the proposal phase.**

### Lint

Run on request, periodically. Health-check pass:

- Contradictions between Base Notes (especially personal facts that may have been superseded).
- Stale claims — a source that has since been challenged by newer ingests.
- Orphan pages with no inbound links.
- Important concepts mentioned in Sources/Daily Notes that lack a Base Note.
- Missing cross-references.
- `04 Indexes/Wiki Index.md` entries with broken links.

Output a punch list; user decides what to act on. Append a `lint` entry to the Log.

---

## Personal Tracking

This is a sub-domain of the wiki, not a separate vault.

**What counts as a personal fact:** atomic, slow-changing truths about the user — preferences, baselines (sleep, energy, focus), what works/doesn't, recurring patterns, decisions made and why, identity statements, recurring failure modes. Frame them like Base Notes: *one fact per note, self-contained, written in the user's voice when quoted*.

**Where they live:** `05 Base Notes/` (flat, not in a `Personal/` subfolder — cross-references with technical notes are valuable). Tag with `personal` and set `visibility: private` in frontmatter.

**Naming:** descriptive title, not "personal_X". E.g. `Sleep Baseline.md`, `How I Learn Best.md`, `Recurring Anxiety Pattern.md`. Keep these in flat `05 Base Notes/`.

**Authorship:** Curate mode is the default for personal Base Notes — the user writes them, the agent collates. But Draft mode is available when the user says so (e.g. "draft my Sleep Baseline note from the last 30 daily notes"). In Draft mode for personal facts, the agent must use observational voice ("Daily Notes show X across N captures") rather than asserting on the user's behalf — the user converts to first-person on review.

**Surfacing candidates:** when ingesting Daily Notes / Fleeting Notes / Sources, watch for repeated themes (3+ mentions across captures, or strong single-incident signals). Propose: *"This has come up N times — worth a personal Base Note? Here's what I'd collate into it."* Do not auto-create.

**Personal Index:** maintain a section in `04 Indexes/Wiki Index.md` listing all `tag: personal` Base Notes with one-line summaries. Treat it as a self-portrait that compounds.

**Digests:**
- **Weekly digest** (Sunday): scan the past 7 Daily Notes + new Sources. Output to `04 Indexes/Digests/<YYYY-WW>.md`. Sections: *patterns*, *anomalies*, *commitments made*, *contradictions with prior personal facts*, *candidate Base Notes*. Draft only — user reads and corrects.
- **Monthly digest** (1st of month): synthesise weekly digests for the prior month. Same format, longer horizon.

Digests are wiki layer (agent-writable). The Daily Notes they're built from are raw (untouchable).

**Trust rule:** if a recalled personal fact contradicts the user's current statement, *trust the current statement* and update the fact. Personal facts have decay.

**Confidence tags:** every personal Base Note carries a `confidence:` frontmatter field — one of `high`, `medium`, `decaying`. Set on creation. The agent flags `decaying` during Reindex or weekly digest if no reinforcing signal has appeared in Daily Notes / new Sources for 8+ weeks. Decaying notes get listed in the next digest's *Contradictions* section as candidates for refresh, rewrite, or archive. The user decides whether to bump confidence back up, rewrite, or retire the note.

---

## Project ↔ Wiki Bridge

Projects in `07 Projects/` are operationally siloed (project tasks, meeting notes, running notes) but they reference *concepts* the wiki should know about. The bridge:

- When the agent is working in a `07 Projects/<name>/` context (writing project notes, helping with implementation, reviewing decisions), it cross-checks every load-bearing concept against `05 Base Notes/`.
- **If a Base Note exists** that's relevant to the project work, link to it from the project note.
- **If a Base Note does not exist** for a recurring concept in the project, propose one (Collate-style). Don't auto-create — projects often invent throwaway terminology that shouldn't pollute the permanent layer.
- During **Reindex**, scan `07 Projects/*/Notes.md` for terms repeated across 2+ projects with no Base Note. Those are strong promotion candidates — knowledge that's accumulated in project silos but belongs in the wiki.
- Project notes themselves stay in `07 Projects/`. The wiki layer only absorbs the *generalisable* concepts.

The point: prevent project work from being a leak. If you learn something while doing cloaksdb, it should compound into the wiki, not stay trapped in the project folder.

### Project session mechanics

Each project in `07 Projects/<name>/` carries three agent-maintained files so sessions aren't amnesiac:

- **`Notes.md`** — living overview: current state, architecture, load-bearing decisions. Shared ownership — agent proposes diffs, user owns it. Load-bearing decisions get a `## Decisions` section (ADR-lite: *Context → Decision → Why → Status*); superseded decisions are marked `superseded by [[…]]`, never deleted.
- **`LOG.md`** — append-only session log, **newest first**. One dated entry per working session: `## [YYYY-MM-DD] — <title>` with **What changed**, **Decisions** (+why), **Learnings / insights**, **Open / next**. Agent-maintained.
- **`PLAN.md`** — the active plan for in-flight work, written *before* executing (goal, steps, files, open decisions, phase checkboxes). It exists so a context reset or a later session can resume — a plan that lives only in chat is lost. Folded into `LOG.md` and cleared when the work ships.

**Session workflow:** (1) *Orient* — read `Notes.md`, the top 2–3 `LOG.md` entries, and `PLAN.md`; the latest `## Open / next` is the starting point. (2) *Plan* — non-trivial work goes to `PLAN.md` before execution. (3) *Execute* — keep `PLAN.md` ticking. (4) *Log* — prepend the session entry to `LOG.md`, written for a reader who wasn't there. (5) *Sync* — propose a `Notes.md` diff if project state changed. (6) *Promote* — flag generalisable learnings for the wiki.

**Interop:** promoted Base Notes cite the originating `LOG.md` entry in `sources:`. Project unknowns go to `04 Indexes/Open Questions.md`, not a separate silo. `/digest` may scan recent project `LOG.md` entries. Keep the two logs distinct — `04 Indexes/Wiki Log.md` records vault-wide ops; a project's `LOG.md` records session work inside one project; a promotion touches both.

**Meta-learnings** (how to work, not what the code does — a prompt pattern, an approach that worked unusually well, a workflow that kept failing) are logged in `LOG.md` under *Learnings*. Recurring ones graduate to either a Base Note (knowledge worth keeping) or a `CLAUDE.md` co-evolution edit (a rule the agent should always follow) — the latter when the same correction recurs.

Full reference: [[Working with Claude]] in `04 Indexes/`.

---

## Conventions

- **Frontmatter on every wiki page:** `created`, `tags`, `visibility` (`private`/`public`), `summary` (one line), `links` (when relevant). Use existing Base/Paper/Project templates as defaults.
- **Source provenance** (Base Notes only): `sources: [[Source Note 1]], [[Source Note 2]]` lists every Source Note that contributed material. Maintained by the **Ingest** op — when a source is absorbed into a Base Note, append it here. Enables traceback: when a source is challenged, grep `sources:` to find every Base Note depending on it. This is the engineering answer to lossy-compression risk.
- **Confidence** (Personal Base Notes only): `confidence: high | medium | decaying` — see *Personal Tracking → Confidence tags*.
- **Status tags** (`#Inbox`, `#Working`, `#Done`) preserved per existing convention.
- **Wikilinks** for all cross-references — `[[Note Name]]` not full paths, unless inside `02 Sources/` where relative paths are already used.
- **Dates** in YAML are ISO `YYYY-MM-DD`. In log entries: `## [YYYY-MM-DD] <op> | <subject>`.
- **Voice:** Base Notes are written in the user's voice (synthesis). Source notes are reportorial. Digests are observational — "this week showed X", not "you should do Y".
- **Never silently rewrite.** Big edits to existing pages should be diffs the user can review, not surprise overhauls.
- **Pocket-jot / Telegram captures land in raw layers.** Don't intercept and "improve" them on arrival.

---

## What NOT to do

- Don't author Base Notes from scratch on speculative or personal topics without user assent — *Collate first, write second*. The user often wants to author the note themselves; the agent's value is deciding what feeds in.
- Don't edit Daily Notes, journal text, or fleeting captures. Read-only.
- Don't bulk-reorganise existing notes without explicit instruction.
- Don't fabricate citations. Every claim in a wiki page traces to a source note, a Daily Note, or the user's stated input.
- Don't compress or summarise Sources to the point that caveats, dates, or minority views are lost. Source notes preserve nuance; Base Notes synthesise.
- Don't gate-keep — if the user wants to break a convention here, they win. Update this file.

---

## Co-evolution

This file is a contract, not a constitution. When a workflow consistently fails or the user repeatedly corrects the same behavior, update this file. Append a brief note to `04 Indexes/Wiki Log.md` recording the change.
