---
title: Working with Claude
created: 
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

## The two layers — and why they have opposite economics

*The single most useful thing to understand about this vault. Decided; it had been the unwritten rationale behind the Study op and the Curate default for a day before it was written down anywhere.*

The vault does two different jobs, and **an agent-drafted note is excellent at one and near-worthless at the other:**

| | **Execution layer** | **Learning layer** |
|---|---|---|
| What a note is *for* | serving the board — a means to a decision | **the note *is* the output** |
| Good agent-drafted note? | **Yes.** Read it, act, move on. The document is the point. | **No.** *The writing is the learning.* A note Claude wrote hands you a document and keeps the understanding. |
| Default mode | Draft | **Curate** |
| Examples | design specs, competitive analysis, project memory, strategy synthesis | anything you want to *think with* later — concepts, mental models, the things you'd want to still hold in a year |

The failure this prevents, in the user's words: *"if I want to learn the note, or think about a problem, **I need to pay attention to it**."* And the diagnosis behind the whole thing: *"**I think killer is collecting too much and never visiting.**"*

So the rule: **Draft mode is legitimate only in the execution layer.** Reaching for it in the learning layer produces a note nobody learned anything from — legible, plausible, and inert.

## The operations

| Op | Trigger | Who does what | Layer |
|----|---------|---------------|-------|
| **`/ingest`** | User points at a `02 Sources/` note | Claude does all of it — Base Notes, provenance, Index, MOC, Log; flips `#Inbox` → `#Done` | Bookkeeping |
| **`/collate`** | About to write a Base Note | Claude searches **the vault**, clusters, proposes a skeleton. **Propose-only — no writes.** *You* write the note | **Learning** |
| **`/study`** | "I want to understand X" | Claude fetches **the world** — finds sources, writes the source notes, collates a skeleton — **then stops.** *You* write the Base Note | **Learning** |
| **`/draft`** | "You write it" / "go ahead" | Claude writes the whole note, every claim cited. You review | Execution only |
| **`/query`** | A question against the wiki | Claude answers with `[[links]]`, logs gaps to Open Questions. You judge | Either |
| **`/lint`** | On demand | Claude proposes a punch list. You pick | Bookkeeping |
| **`/reindex`** | Monthly-ish | Claude proposes merges/splits/MOCs. You pick | Bookkeeping |
| **`/digest`** | Weekly (Sun) / monthly (1st) | Claude scans, observes. You correct | *Has never once run* |

**Collate searches the vault; Study fetches the world.** Both stop before the note gets written — that stop is the point, not an omission.

The Study op's explicit failure condition: **if you finish a Study having read a good note instead of written a bad one, the op failed.**

`/collate`, `/study`, `/lint` and `/reindex` are **propose-only** in their first phase. Claude writes only what you accept, one item at a time, with diffs.

## Curate vs Draft mode

Every Base Note is authored in one of two modes:

- **Curate** — Claude collates and proposes structure; **you write** in your own voice; Claude polishes, cross-links, indexes. **The default whenever the point is that *you* end up understanding something** — which is every personal or reflective topic, and every concept you want to think with later.
- **Draft** — Claude writes the whole note with cited `[[links]]`; you review and edit. **For the execution layer only**, where the document is the deliverable and nobody needs to have learned anything by writing it.

Triggers: "draft it" / "write the note" / "go ahead" → Draft. "collate" / "what should I include" / "I'll write it" → Curate. Unclear → ask once.

> [!warning] **Where this currently stands.** Curate mode has **never been used**. Every Base Note written since the contract was adopted — thirteen of them — was agent-drafted, and **none has ever been accepted**. The queue is 11 drafts, 0 accepted, 0 rejected. That is the execution layer eating the learning layer, and it is what the split above exists to stop.

## Which files are yours, and which are mine

*Also decided in conversation once and never written down — the reason the vault feels overwhelming is partly that nobody ever said which pages you're supposed to read.*

**Your read surfaces — these are for you:**

| File | When to read it |
|---|---|
| **[[Current WIP]]** | **Daily.** The one page that says what to do next. If you read nothing else, read this. |
| **[[Open Questions]]** | The research backlog. When choosing what to dig into. |
| **[[Ventures]]** | *"When the pile feels confusing, not daily."* It answers "what is all this" — the board answers "what do I do now." |
| **`08 Trackers/Review Queue.base`** | When judging drafts. |

**My bookkeeping — you should never need to open these:**

`Wiki Log` (my audit trail, so you can check and revert what I changed) · `Wiki Index` (the catalog I search) · `Wiki Map` (domain shape, regenerated on Reindex).

If you find yourself reading my files to work out what's going on, that's a bug in *your* surfaces — say so, and the fix belongs in `Current WIP` or `Ventures`, not in a habit of reading the log.

## Ceremony is my job, not yours

Structure that taxes capture is worse than no structure — *"the point of failure isn't a messy vault, it's a vault you stop writing into."* So: templates stamp `#Unfiled` and leave `summary`, `tags`, `links`, `sources` and `Origin` deliberately blank. **I never ask you for a tag** — I guess, state the guess, and move on. Triggers: **"file this"**, **"shorten this."** Write badly and fast; the filing is mine.

**`Base.md` no longer prompts for a title**. New note → start typing; there is nothing between you and the thought. Naming is filing, so it's my job: *"file this"* names an `Untitled` note, syncs the frontmatter title, fills the blanks and clears `#Unfiled`. The four templates that still prompt — `Paper`, `Books`, `Movies`, `Project` — keep it on purpose: a paper's title isn't a decision you're making, it's one you already have.

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

Projects in `07 Projects/<name>/` are operationally siloed but they shouldn't be amnesiac. Each project session should leave a trail Claude can pick up next time without re-deriving context. Four files per project carry that:

| File | Role | Who writes |
|------|------|------------|
| **`Notes.md`** | Living overview — current state, architecture, subsystem map. The "where things stand" doc. Holds a short pointer to `DECISIONS.md`, not the decisions themselves. | Shared. Claude proposes diffs; user owns it. |
| **`LOG.md`** | Append-only session log, **newest first**. One dated entry per working session. | Claude maintains. |
| **`PLAN.md`** | The active plan for in-flight work. Survives context loss so work can resume. Cleared/archived into `LOG.md` when the work ships. | Claude maintains. |
| **`DECISIONS.md`** | Load-bearing decisions **and the active constraints they imply** — the do/don't rules to check before editing. Created when the first load-bearing decision appears. | Claude proposes; user confirms. |

**The loop, in one line:** *orient (read) → plan (`PLAN.md`) → execute → log (`LOG.md`, before compaction) → sync (`Notes.md`) → promote (wiki).* The sections below expand each step; an agent that internalises this line can derive the rest.

(Existing example to match: [[Obsidian SSH/LOG]] — dated entries with **What changed / Decisions / Learnings / Open / next**, newest first. Note its older entries use ad-hoc `P0/P1/P2` headers; the current format is the four bold fields, not priority grouping.)

### Session-start checklist

Before doing project work, Claude runs this — it's the "orient" step made explicit:

- [ ] Read `Notes.md` — current state, architecture, decisions.
- [ ] Read the top 2–3 `LOG.md` entries — what recent sessions did and left open.
- [ ] Read `PLAN.md` if it exists — is there in-flight work to resume?
- [ ] Skim `DECISIONS.md` if it exists — the **Constraint** lines are the do/don't rules that must not be violated this session.
- [ ] Check `## Open / next` in the latest `LOG.md` entry — that's the intended starting point.
- [ ] Cross-check load-bearing concepts against `05 Base Notes/` — link what exists, note what should.
- [ ] Confirm the session's goal with the user if `PLAN.md` and the user's ask disagree.

### Session workflow for projects

1. **Orient** — run the session-start checklist above. That's the working context; don't re-derive it.
2. **Plan** — for anything non-trivial, write the plan to `PLAN.md` *before* executing: goal, steps, files touched, open decisions. If the user approves a plan in-session, it lands here so a later session (or a context reset) can resume it.
3. **Execute** — do the work. Keep `PLAN.md` ticking — check off steps, note deviations.
4. **Log** — at the end of the session, *and before any auto-compact*, prepend (or refresh) a dated entry in `LOG.md`:
 - `## [YYYY-MM-DD] — <session title>`
 - **What changed** — the deltas a diff *won't* explain (the why, the surprises). Don't hand-transcribe the file-by-file change list — `git log` already has that.
 - **Decisions** — choices made and *why* (the reasoning is the valuable part). Load-bearing ones get promoted to `DECISIONS.md` (see below).
 - **Learnings / insights** — see below.
 - **Open / next** — what's unfinished, what's blocked, what the next session should pick up.
 - **Multi-idea sessions:** if the session covered more than one thread, give each its own `**Thread: <name>**` sub-block. A big tangent that won't finish now doesn't get buried in prose — it becomes an `## Open / next` item or a fresh `PLAN.md` stub, so it's resumable.
5. **Sync `Notes.md`** — if the session changed the project's overall state or architecture, propose a diff to `Notes.md`. `LOG.md` is the history; `Notes.md` is the current truth.
6. **Promote** — generalisable learnings get flagged for the wiki (see below). When `PLAN.md` work is fully shipped, fold its outcome into the latest `LOG.md` entry and clear the file.

### Plans, summaries, and learnings

- **Saved plans** live in `PLAN.md` — never only in chat. A plan that exists only in conversation is lost on context reset. If a plan is large or multi-phase, keep phase checkboxes in `PLAN.md` so progress is visible across sessions.
- **Session summaries** are the `LOG.md` entry itself — that *is* the summary. Write it for a reader who wasn't there: enough that next session's orientation step is just "read the log."
- **Learnings** split two ways:
 - **Project-specific** (a gotcha in this codebase, a config quirk, a failure mode) → stays in `LOG.md`, or graduates to `Notes.md` / a project `Failure Modes.md` if it's load-bearing. (See [[`<repo>`/Failure Modes]] for the pattern.)
 - **Generalisable** — an interesting technique, a reusable approach, a non-obvious insight, *an interesting way a task got solved* — → flagged for promotion to a `05 Base Notes/` page via the Project Bridge. Claude **proposes**, doesn't auto-create — projects invent throwaway terminology that shouldn't pollute the permanent layer. During `/reindex`, terms repeated across 2+ projects with no Base Note are strong promotion candidates.
- The test for "is this a wiki learning or a project log entry": *would this help on a different project?* If yes, propose it upward. If it's only true inside this repo, it stays in the project.

### Writing the log before auto-compact

Step 4 above says "before any auto-compact" — this is why it matters. The `LOG.md` entry isn't a session diary written once at the end; it's **the memory that outlives the context window.** Auto-compact often means there is no clean "session end": context fills, compaction fires, and the pre-compaction reasoning (the *why* behind what was done) is exactly what gets summarised away.

- **Treat "approaching compaction" as a checkpoint, not just session end.** When context is getting full, append or refresh the current `LOG.md` entry *from full context first*. A session that compacts three times should touch the log three times.
- **Never let compaction be the first summarisation of the session.** You summarise it deliberately into the log; you don't let the compactor do it lossily for you.
- **Checkpoints can be terse.** A pre-compact checkpoint may be a running scratch of decisions + open threads; clean it into a proper entry at true session end.
- **Mechanism (no app code):** a `PreCompact` hook in `settings.json` injects a "write/refresh the LOG entry now" reminder at the compaction boundary — the same trigger pattern as the per-repo `CLAUDE.md`. Relying on Claude to *remember* to log is weaker than a hook that fires at the boundary. Installed via `second-brain-skills` (it owns `~/.claude/` wiring).

### Decision records — `DECISIONS.md`

Most decisions live fine as a `**Decisions**` line in a `LOG.md` entry. But a decision that is **load-bearing** — it shapes the architecture, it'll be questioned later, reversing it is expensive — gets promoted to a dedicated `DECISIONS.md` so the *why* doesn't get buried in chronological log scroll, and so the **constraint it implies** is captured right next to it.

- **Where:** a dedicated `DECISIONS.md` at the project root (not inside `Notes.md` — `Notes.md` keeps only a short pointer). Newest first.
- **Stable ids + referents.** Each decision is `### D-NNN — <title>` and carries a **`Referent`** — the `path/glob` · `symbol` · `subsystem` it binds. Referents must be concrete and greppable: they are how a decision is retrieved at the moment it matters (by a person grepping, or by a memory layer indexing the repo). An id never changes and never gets renumbered, even when superseded.
- **Format** (ADR-lite): `### D-NNN — <title>` → **Status** (`accepted` / `superseded by D-NNN` / `revisited`) → **Referent** → **Context** (what forced the choice) → **Decision** (what was chosen) → **Why** (alternatives rejected) → **Constraint** (the do/don't imperative the decision implies — the thing to check before editing the referent).
- **The Constraint line is the distillation, kept *on* the decision.** A decision is "we chose clock-not-LRU eviction"; its constraint is "don't add a second eviction path." Keeping the constraint on the decision rather than in a separate registry means the rule and its rationale never drift apart — and the Constraint line is exactly what a `PreToolUse:Edit` memory layer would inject before the model writes.
- **When Claude writes one:** propose it at log-time when a session's `**Decisions**` line is clearly load-bearing — don't silently inline a major architectural call and move on. The user confirms.
- **Superseding, not deleting:** when a later decision overturns an earlier one, mark the old record `superseded by D-NNN` (and retire its Constraint) rather than removing it. The reversal history is itself valuable.
- **Wiki link:** if a decision rests on a concept with a Base Note, cite it. If it *establishes* a generalisable principle, that's a promotion candidate.

### How the repo is wired to the vault

*The mechanism, in one place. User-facing version: [[00 Vault Guide]] §Code Repos and Project Memory.*

- **Memory files are canonical in `07 Projects/<name>/` and symlinked into the repo root** — `Notes.md`, `LOG.md`, `Todo.md`, `PLAN.md`, `DECISIONS.md`. The repo gitignores them. **Never write one repo-only:** a forked copy is invisible to the vault, and that is exactly how a project falsification was lost for a day.
- **`AGENTS.md` is the repo's agent contract** — model-agnostic, git-tracked. `CLAUDE.md`, `GEMINI.md`, `.cursorrules` are relative symlinks to it, so the choice of tool is not a fork. Its top region is **generated** from `99 Templates/Project AGENTS.md`; **to change what every project tells its agent, edit the template and run `sync` — never edit the generated region in a repo.** Project-specific instructions live below the closing marker.
- **`.vault/`** — a gitignored symlink to the vault root in every adopted repo, so an agent working in the repo can reach this page and [[Current WIP]]. Before it existed, the contract instructed a repo-side agent to promote learnings and update the board while giving it no path to either.
- **`scripts/vault-project adopt | sync | check`** is the only supported way to wire this. `check` prints `adopted N/M`, names any forked memory file, flags a **stale board** (a project `LOG.md`/`DECISIONS.md` dated newer than its `Last:` stamp on [[Current WIP]] means a state change never reached the surface where the user acts), and **exits 1**. Rules belong in the template; **coverage belongs in the script** — replicating a rule into thirteen repos makes it thirteen times more visible and zero times more true.
- **`adopt`/`sync` never commit.** A `git add -A` in this script once swept 457 lines of another session's real work into a commit called *"Adopt vault project scaffolding"* (`<repo>` `a2e079c`; the same mistake hid a 925-line diff under a project `8a88ff5`). **Never `git add -A` in a repo you didn't do the work in** — wire the files, let the user commit their own work with its own message.

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

### General principles — working on projects with Claude

The Notes/LOG/PLAN mechanics above are *this vault's* convention. The principles below are vault-agnostic — they hold for any project Claude works on, and they're the thing to keep in mind when the mechanics don't obviously cover a situation.

- **Orient before acting; don't re-derive what's written down.** The first move in any session is to read the existing context (`Notes.md`, recent `LOG.md`, `PLAN.md`, the actual code) rather than reconstruct it from memory or assumption. Most wasted work comes from starting before understanding where things stand.
- **Scope a session to one shippable thing.** A session should have a single goal you can name and finish. "Do the rest" is not a goal — break it down. Unfinished scope gets finished now or written into `## Open / next`, never left implicit.
- **Plan in writing before non-trivial execution.** If the work has more than a couple of steps or any open decisions, the plan goes in `PLAN.md` *first*. A plan that lives only in the conversation is lost on the next context reset.
- **Ask when the decision is genuinely the user's; otherwise pick the sensible default and say so.** Stop and ask when a choice changes *what* gets built, depends on the user's intent/priorities, or is expensive to reverse. For conventional choices with an obvious default, proceed and state the assumption — don't manufacture a question.
- **Keep changes reviewable.** Prefer small, coherent diffs that match the surrounding code's style and idiom over large rewrites. Big edits should be diffs the user can accept or reject, not surprise overhauls — the same "never silently rewrite" rule the wiki layer follows.
- **Report outcomes faithfully.** If tests fail, say so with the output. If a step was skipped, say that. "Done" means done *and verified* — state that plainly, and hedge only when something is genuinely unverified. Never claim a result you didn't observe.
- **Confirm before irreversible or outward-facing actions.** Deleting/overwriting files you didn't create, pushing, publishing, anything hard to undo — confirm first unless explicitly told to proceed. Approval for one such action doesn't carry to the next. Before deleting or overwriting, look at the target: if it contradicts how it was described, surface that instead of proceeding.
- **The why is the durable part.** When recording a decision, the reasoning (what was rejected and why) outlives the decision itself. A choice without its rationale gets re-litigated; a choice with it can be confidently kept or overturned. Supersede, don't delete.
- **Don't let project work become a knowledge leak.** A learning that would help on a *different* project belongs in the wiki, not trapped in the project folder. The promotion test — "would this help elsewhere?" — applies to every non-obvious thing learned, not just code.
- **Surface contradictions, don't paper over them.** If new work conflicts with a prior decision, a Base Note, or what the user just said, flag it. The trust rule applies: a current statement beats a stale recorded fact, but the conflict gets named, not silently resolved.

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
