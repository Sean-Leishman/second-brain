---
title: CLAUDE.md
created: 
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
| **Raw (immutable to agent)** | `01 Fleeting Notes/`, `02 Sources/`, `06 Daily Notes/`, pocket-jot/Telegram captures, **Claude conversation transcripts** | User (or capture pipeline). Agent reads only. |
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
- **`04 Indexes/Wiki Log.md`** — chronological record, **newest first: prepend new entries directly below the header, never append at the bottom.** Format: `## [YYYY-MM-DD] <op> | <subject>` so it's greppable. Ops: `ingest`, `query`, `lint`, `reindex`, `digest`, `project`. The Log is *history*, never the instruction — see *The board is not the log*.
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

#### Conversations are a source 

**A Claude conversation is raw material like any article, and it is the densest one.** Decisions get made in chat — a strand parked, a rule rewritten, a persona disbelieved — and the artifact that reaches the vault records the *rule* while the *reasoning* stays in a transcript nobody opens. That is a leak, and once it bit hard: the Study op and the ceremony clause were argued out in a `<repo>` session, and a later vault session re-derived the same conclusion from scratch because it had read the contract but not the conversation.

- **Read them:** `scripts/transcript-digest [YYYY-MM-DD]` lists a day's conversations; `scripts/transcript-digest <id>` prints one (user turns verbatim + the agent's substantive replies).
- **Ingest them:** short source notes in `02 Sources/Conversations/`, one per substantive conversation. Reportorial, capped short, **the user's words quoted verbatim — never paraphrased into agent prose.** Every note carries a *"Never reached the vault"* section: which decisions exist only in that transcript. That section is the actionable output.
- **Skip the trivia.** A config-fix session is not a source. Say what was skipped.
- Transcripts themselves are **immutable** — they are the record of what was actually said.

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

**Collate searches the vault, not the world.** If the vault has nothing on the topic, Collate returns nothing — that is not a failure, it is the signal to run **Study**.

### Study 

**Trigger:** *"study X"*, *"I want to learn X"*, *"teach me X"*, *"help me think about X"* — a topic the user wants to **understand**, as opposed to a decision they want to **make**. Collate answers *"what do I already know about X"*; Study answers *"I don't know X yet."*

**The rule that governs the whole op: the agent fetches and organises; the user writes.** In the learning layer the note *is* the output — the writing is where the understanding happens, so an agent-drafted Base Note hands the user a document and keeps the learning. **Study is Curate mode with a research front-end. Never Draft mode**, unless the user explicitly overrides.

1. **Scope it.** One or two clarifying questions, only if the topic is genuinely ambiguous. Otherwise start.
2. **Find the real sources — fetch them, never summarise from memory.** The canonical paper, the primary spec/doc, the one good explainer. Prefer primary over secondary; prefer the thing that argues over the thing that reviews. **Say plainly which claims are model-knowledge and which are fetched** — a Study built on recollection is exactly the slop this vault is designed to keep out.
3. **Write the source notes** into `02 Sources/` (agent-writable on explicit ingest — this is that). One note per source, reportorial voice, honest about what it does and doesn't establish.
4. **Collate them into a skeleton** for the Base Note: the core concepts, the places sources disagree, what's genuinely unresolved, and — the useful part — **what the user already has in the vault that connects** (`[[links]]` to existing notes).
5. **Stop. The user writes the Base Note**, in their own words, from the skeleton. Badly is fine. Then `file this` and the agent does the ceremony.
6. **Optional, and worth offering:** after they've written it, the agent reads it back and says where the understanding looks thin — *not* by rewriting it, but by asking the questions the sources would ask. Testing beats re-reading.

**What Study must not do:** write the Base Note; pad the skeleton into prose; fetch twenty sources when three would do; or produce a summary so complete the user never needs to think. **If the user finishes a Study op having read a good note instead of written a bad one, the op failed.**

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

The point: prevent project work from being a leak. If you learn something while doing a project, it should compound into the wiki, not stay trapped in the project folder.

### Project memory lives in the vault 

`Notes.md`, `LOG.md`, `Todo.md`, `PLAN.md`, `DECISIONS.md` are **canonical in `07 Projects/<name>/` and symlinked into the code repo root** (the repo gitignores them). The repo also carries an `AGENTS.md` whose *Project memory* section points at them — the symlink is the mechanism, the `AGENTS.md` section is what makes an agent read it. Neither works alone.

**Never write a project memory file to the repo only.** A forked copy is invisible to the vault, and the wiki cannot reason about what it cannot see.

**`AGENTS.md` is the canonical agent contract, and it is model-agnostic.** `CLAUDE.md`, `GEMINI.md` and `.cursorrules` are *relative* symlinks to it inside the repo, so every tool reads one file and the choice of model is not a fork. Its top region is generated:

```
<!-- vault:shared:begin --> … rendered from `99 Templates/Project AGENTS.md` — do not edit in the repo
<!-- vault:shared:end --> … everything below this line is project-specific and survives syncs
```

`scripts/vault-project` is the only way this is wired — never hand-roll the symlinks:

| Command | What it does |
|---|---|
| `vault-project adopt <repo> [name]` | Register a repo. Moves any existing memory files *into* the vault, seeds what's missing from `99 Templates/`, symlinks them back, gitignores them, folds an existing `CLAUDE.md` into `AGENTS.md`. |
| `vault-project sync [name…]` | Re-render the shared region in every registered repo. Idempotent. **This is how a template change ships.** |
| `vault-project check` (= `list`) | **The coverage check.** Prints `adopted N/M`, names every unadopted project, and flags any repo with a *forked* memory file the vault cannot see, a stale `AGENTS.md`, or no `.vault/` link. **Exits 1** when anything is wrong, so it can gate a hook or CI. |

**Rules belong in the template; coverage belongs in the script.** A rule written into `99 Templates/Project AGENTS.md` is an *assertion* — replicating it into 13 repos does not make it true in any of them. That is the failure this whole mechanism exists to prevent (`Current WIP` asserted "symlinked so that can't recur" while it held for 2 of 13). So: the template says what an agent should do; **`vault-project check` is the only thing entitled to say whether it happened.** Never write a coverage claim into a note or the board — write the command that prints it.

**To change what every project tells its agent, edit `99 Templates/Project AGENTS.md` and run `vault-project sync`.** Never edit the generated region in a repo — the next sync overwrites it. To change the template's *structure* (a new memory file, a renamed one), edit `SEED`/`LINK` in the script and re-sync; it creates what's missing but will not delete what's been retired — do that by hand.

**The repo can reach the vault.** `adopt`/`sync` also drop a gitignored `.vault/` symlink at the repo root pointing at the vault root, and the shared region names the paths worth reading: `.vault/04 Indexes/Working with Claude.md`, `.vault/CLAUDE.md`, `.vault/00 Vault Guide.md`, `.vault/08 Trackers/Current WIP.md`, `.vault/04 Indexes/Wiki Index.md`, `.vault/05 Base Notes/`. Without this the contract was unenforceable — it told a repo-side agent to promote learnings and update the board while giving it no path to either. *The vault's own rules bind an agent arriving through `.vault/`:* raw layers stay read-only, Base Notes are proposed and not silently created.

Registry: `07 Projects/registry.tsv` (`vault-folder<TAB>repo-path`).

### The board is not the log 

**A session that changes a project's status — above all a kill, a falsification, or a shipped premise — updates `08 Trackers/Current WIP.md` in the same pass.** Not the next session. Not "when the user asks."

Writing it to a `LOG.md` or to `Wiki Log.md` is *not* sufficient: those are history, the board is the instruction. A finding that doesn't reach the board doesn't exist.

**Each Active line carries a `Last:` stamp.** One italic sub-line: **the most recent thing that actually happened, dated.** It answers *"where did I leave this?"* without opening anything.

- **The agent writes it at session end**, in the same pass as the `LOG.md` entry. Never ask the user to update it.
- **One line. The full story is never on the board** — it is in that project's `LOG.md`. The stamp is a pointer plus a date, not a history.
- **It must say what happened, including when nothing did.** *"Last: — application drafted. Not filed. Nothing has started its clock."* An item that has been still for weeks should read as still. A board where every line looks busy is a board that lies.
- **Consistency check (this is what makes the stamp worth having):** if a project's `LOG.md` has an entry newer than its board `Last:` stamp, **the board is stale — that is a bug, fix it in the same pass.** This is the tripwire for the exact failure below.

*Why this rule exists:* once, a project's central hypothesis was falsified — three legs shipped, two negative results, v0 premise dead. It was logged to a repo-only `LOG.md` and summarised in `Wiki Log.md`. `Current WIP.md` was never touched, so for a full day the board went on telling the user to go do the central hypothesis that had already run and already failed — and the Reindex once propagated that dead state into a brand-new `Ventures.md` because it trusted the board. Two files disagreeing is a bug; the board losing is the worst case.

### One current truth, and the change is explicit 

**A note leads with what is true now. When a verdict changes, the change is stated in the note — not stacked as a new section, and not silently deleted either.**

The failure this rule exists to stop: `another project.md` reached 372 lines carrying `## Verdict`, `## Verdict (revised)` and `## VERDICT — REVISED AGAIN` **simultaneously, each contradicting the last**, plus callouts apologising for errors in a draft nobody would ever read again. Impossible to open and know what was true. Agents write fast; append-only editing turns that speed straight into unreadability.

**The rules:**

1. **One current-truth section, at the top.** New verdict replaces old verdict *in place*. Never "REVISED AGAIN".
2. **But the reversal stays visible — one line, in the note:** *"Was X; flipped to Y on `<date>` because `<reason>`."* A superseded verdict is not an error to hide; it is a fact about how the thinking moved. **If the old view has its own note, keep it and link the two so the disagreement stays navigable.**
3. **Real corrections are content; apologies aren't.** If a research pass finds an earlier claim wrong, fix the claim, and state the correction if it changes what a reader should believe. Don't leave a callout addressed to a version of the note nobody read.
4. **Keep it readable in one sitting.** A Base Note past ~150 lines is usually two notes. Length is a bug report about the note, not a feature of the topic.
5. **`LOG.md` and `Wiki Log.md` are append-only, newest-first.** History is their whole job.

> [!warning]- **Why this was revised within hours of being written **
> The first version said: *delete the old verdict, git log is the archive.* A research pass killed it. **No source in either the classical or the agent-native lineage endorses git-as-knowledge-archive, and Zettelkasten explicitly opposes it.** Bob Doto: *"To throw out or delete notes simply because they no longer seem relevant now is to create a temporally-bound zettelkasten... you've erased your past self while severely handicapping the self you have yet to become."*
> The decisive point is not recoverability — it is that **his remedy is in-vault.** Keep the superseded idea and *link* the contradiction, so it stays navigable and can resurface serendipitously. **A git commit preserves the bytes but removes the note from the live link graph**; it answers a recoverability objection Zettelkasten was never making.
> **So: current truth leads, but the change is explicit and stays in the vault.** This note is itself the worked example — the rule that was wrong is still here, one fold away, linked to what replaced it.

### Ceremony is the agent's job 

**The user writes prose. The agent does the filing.** Frontmatter, `links:`, wikilinks, status tags, `Wiki Index` lines, MOC upkeep, `Wiki Log` entries, banner callouts, superseding old notes — all of it is mechanical, and none of it should ever cost the user a minute.

*Why:* the point of failure isn't a messy vault, it's a vault the user stops writing into. When the cost of *filing* a thought exceeds the cost of *having* it, thoughts stop arriving. Structure that taxes capture is worse than no structure.

**The mechanism: `#Unfiled`.** `99 Templates/Base.md` — auto-applied by Templater to anything created in `05 Base Notes/` or `01 Fleeting Notes/` — stamps a new note **`#Unfiled`** and leaves `summary`, `tags`, `links`, `sources` and `Origin` **deliberately blank. Those are the agent's fields, never the user's.** The tag makes the backlog a live view: **`08 Trackers/Unfiled.base` → *Needs filing***.

**The `file this` op, in full:**

1. Read the note. Fill `summary` (one line: what it *says*, not what it's *about*), `tags`, `links` (real wikilinks to notes that exist), `sources` if any, and the `Origin` line.
2. Move it to the right folder if it's in the wrong one.
3. Add its line to `04 Indexes/Wiki Index.md` and any topic MOC it belongs in.
4. Prepend an entry to `04 Indexes/Wiki Log.md`.
5. **Replace `#Unfiled`** with the right lifecycle tag: `#Inbox` (raw capture), `#Working` (live thinking), `#Draft` (**only** if the agent wrote the body).
6. If it changes a project's status, update `08 Trackers/Current WIP.md` in the same pass — see *The board is not the log*.

**Triggers — full authority to do all of the above, no questions:**

- **"file this"** / **"tidy this"** / **"do the ceremony"** — on a note the user just typed, or raw text pasted into chat. **Ask nothing. The user corrects afterwards if it's wrong.**
- **"shorten this"** — apply *Overwrite, don't append*: collapse stacked verdicts, cut history git already holds, keep current truth.
- **Any note carrying `#Unfiled`** is a standing filing job — if you're doing vault work and one is sitting there, file it. Don't ask whether they want it filed.
- A note the user typed with no frontmatter is not an error to report back. **It's a filing job. Just do it.**

The user's *words* stay theirs (Roles, above — never rewrite their voice). The *scaffolding* around those words is the agent's, always.

**Never ask the user to supply a tag, a summary, a link, or a folder.** If you can't infer one, guess and state the guess in one line. A wrong guess costs them three seconds to correct; a question costs them the habit.

---

## Conventions

- **Frontmatter on every wiki page:** `created`, `tags`, `visibility` (`private`/`public`), `summary` (one line), `links` (when relevant). Use existing Base/Paper/Project templates as defaults.
- **Source provenance** (Base Notes only): `sources: [[Source Note 1]], [[Source Note 2]]` lists every Source Note that contributed material. Maintained by the **Ingest** op — when a source is absorbed into a Base Note, append it here. Enables traceback: when a source is challenged, grep `sources:` to find every Base Note depending on it. This is the engineering answer to lossy-compression risk.
- **Confidence** (Personal Base Notes only): `confidence: high | medium | decaying` — see *Personal Tracking → Confidence tags*.
- **Status tags** (`#Inbox`, `#Draft`, `#Working`, `#Done`) preserved per existing convention. They are real Obsidian tags even when written in the Properties callout body, so they are queryable from a Base — `08 Trackers/Review Queue.base` is the live review board.
- **Draft-mode review signal:** agent-drafted notes carry **`#Draft`** + an `Origin: Draft mode — user to review` line in Properties. `#Draft` is a queryable status tag, so the review backlog is a live view (`08 Trackers/Review Queue.base` → *Awaiting verdict*) rather than a prose line no tracker can see; the ordered queue itself lives on [[Current WIP]]. The lifecycle is `#Inbox` → `#Draft` (agent wrote it, awaiting verdict) → `#Working` (accepted, being extended) → `#Done`; a human-authored note starts at `#Inbox` and never passes through `#Draft`. The review pass resolves each note one of three ways: **accept** — flip to `#Done` and delete the review line (edits welcome first; user edits are authoritative and never reverted by the agent); **park** — leave `#Draft`, review line stays, agent may keep extending it; **reject** — delete the note or replace the review line with `Rejected: <one-line why>` so the reasoning survives. Agents treat any note still carrying the review line as *proposal, not knowledge*: don't cite it as established, don't build new notes on top of it without flagging the dependency.
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
