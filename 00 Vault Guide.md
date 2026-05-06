---
title: Vault Guide
created: 2026-04-04
type: guide
cssclasses:
  - center-images
---
Workflows for this Obsidian vault. Covers the Zettelkasten pipeline, task management, Telegram bot routing, and how digital and analogue systems fit together.

---

## System Overview

A hybrid analogue + digital system. Each medium does what it's best at.

| Medium                                  | What it handles                                                       | Why                                    |
| --------------------------------------- | --------------------------------------------------------------------- | -------------------------------------- |
| **Analogue: Life Tracker** (A5 journal) | Daily journal, habit tracking, reflection, goals, personal philosophy | Slow thinking, mindfulness, no screen  |
| **Analogue: Pocket Jot** (Field Notes)  | Capture fleeting thoughts, quick todos, observations                  | Always on you, zero friction           |
| **Obsidian (this vault)**               | Knowledge management, source notes, project notes, task tracking      | Searchable, linkable, Dataview queries |
| **Obsidian (work vault)**               | Work project notes, meeting notes, work todos                         | Keeps work context isolated            |

**The bridge between analogue and digital is the weekly review.** No OCR. Pocket jot items get triaged into Obsidian Inbox or the Life Tracker journal on Sundays.

---

## Vault Structure

| Folder | Purpose |
|--------|---------|
| `00 Bases` | Database views |
| `01 Fleeting Notes` | Raw captures, unprocessed thoughts — temporary |
| `02 Sources` | Literature notes (Articles, Books, Papers, Videos) |
| `03 Tags` | Tag pages |
| `04 Indexes` | Topic MOCs linking related sources (Piranesi-style index) |
| `05 Base Notes` | Permanent/evergreen atomic notes |
| `06 Daily Notes` | Lightweight daily log (tasks + notes, not journaling) |
| `07 Projects` | Project notes, meetings, and todos |
| `08 Trackers` | Task management + consumption lists |
| `99 Templates` | Note templates |

---

## Zettelkasten Pipeline

Notes flow through four stages. Each stage has a folder.

```
Capture ──▶ Process ──▶ Connect ──▶ Index

01 Fleeting    02 Sources     05 Base       04 Indexes
  Notes       (literature)    Notes          (MOCs)
```

### Stage 1: Fleeting Notes (`01 Fleeting Notes/`)

**Raw, unprocessed captures. Temporary — they exist to be processed, not to live forever.**

What goes here:
- An idea that popped into your head
- A rough braindump on a topic you're exploring
- Unprocessed notes from a conversation or meeting
- Things from Telegram `/note` command

What does NOT go here:
- Finished summaries of papers/videos (→ `02 Sources/`)
- Polished concept explanations (→ `05 Base Notes/`)
- Todos (→ `08 Trackers/Inbox.md`)

**Lifecycle:** Process within days. Each fleeting note either:
1. Becomes a **base note** in `05 Base Notes/` (atomic, self-contained)
2. Gets absorbed into an existing base note
3. Moves to `02 Sources/` if it's actually a source summary
4. Gets deleted

### Stage 2: Source/Literature Notes (`02 Sources/`)

**Processed notes about a specific source — a paper, video, article, book.**

| Subfolder | Template | Created by |
|-----------|----------|------------|
| `Papers/` | Paper | Manual |
| `Books/` | Books | Manual |
| `Articles/` | Base (or Telegram bot) | Bot or manual |
| `Videos/` | Base (or Telegram bot) | Bot or manual |

Key rule: Written in your own words, not copy-pasted. Summary + key ideas + review questions.

### Stage 3: Base/Permanent Notes (`05 Base Notes/`)

**Atomic, self-contained explanations of a single concept.**

Rules:
- **One idea per note** — if it covers two concepts, split it
- **Self-contained** — understandable without opening other notes
- **In your own words** — synthesis, not summary
- **Linked** — to related base notes and source notes
- **Tagged** — so index pages can find them

### Stage 4: Index/MOC Pages (`04 Indexes/`)

**Curated navigation pages linking related notes on a topic.** The digital equivalent of Piranesi's separate index — you build it as you go, pointing to sources and base notes.

Structure:
```markdown
- [[../02 Sources/Papers/Paper 1|Paper 1]] — foundational paper on X
- [[../02 Sources/Papers/Paper 2|Paper 2]] — extends Paper 1 with Y
- [[../05 Base Notes/Concept|Concept]] — key idea from this area
```

When to create: 3+ sources on same topic, or starting a new research area.

### Processing Fleeting Notes

Fleeting notes are temporary. The core pattern: **read → decide → create/merge → link → delete**.

**Decision tree:**

```
Is it about a specific source (paper/video/book)?
  YES → 02 Sources/
  NO ↓

Is it a self-contained concept you can explain standalone?
  YES → 05 Base Notes/ (new or merge into existing)
  NO ↓

Is it research/work for a specific project?
  YES → 07 Projects/<name>/Notes.md
  NO ↓

Is it a todo or action item?
  YES → 08 Trackers/Inbox.md
  NO ↓

Is it multiple things mixed together?
  YES → Split and route each piece above
  NO ↓

Is it junk?
  YES → Delete
```

**Fleeting → Base Note (new concept):**
1. Extract the core idea — can you explain it standalone in 6 months?
2. Create note in `05 Base Notes/`, written in your own words
3. Link to related base notes and source notes
4. Tag it, add to relevant `04 Indexes/` if one exists
5. Delete fleeting note

**Fleeting → Existing Base Note (extends something):**
1. Realise this belongs to an existing concept
2. Open the existing base note, add new section or detail
3. If the note gets too long → split into two base notes
4. Delete fleeting note

**Fleeting → Source Note (it was about a paper/video/article):**
1. Create source note with appropriate template in `02 Sources/`
2. Reorganise raw notes by *theme*, not by section of the source
3. Write summary + key ideas + review questions
4. Add to `04 Indexes/`
5. Delete fleeting note

**Fleeting → Project (actionable work):**
1. Create project in `07 Projects/` if it doesn't exist
2. Move research content to `Notes.md`
3. Extract actionable items to `Todo.md`
4. Link to any `02 Sources/` notes that informed it
5. Delete fleeting note

**Fleeting → Multiple Destinations (braindump):**
Read through, highlight distinct ideas, and route each piece separately. A single fleeting note might produce a base note, a source note, and three inbox items.

### How This Vault Compares to Other Approaches

Several popular note-taking systems use similar concepts with different names. The distinction between **literature notes** (our Source Notes) and **permanent notes** (our Base Notes) is the key one.

| Concept | Zettelkasten (Luhmann) | PARA (Tiago Forte) | This Vault |
|---------|----------------------|---------------------|------------|
| Raw capture | Fleeting notes | Inbox | `01 Fleeting Notes/` |
| Notes *about* a source | Literature notes | Resources | `02 Sources/` |
| Your own ideas | Permanent notes | Notes (in Projects/Areas) | `05 Base Notes/` |
| Navigation | Index cards / hub notes | Areas + PARA folders | `04 Indexes/` |
| Active work | — | Projects | `07 Projects/` |
| Backlog | — | Archives | `08 Trackers/Someday.md` |

**Literature notes vs Permanent notes — the critical distinction:**

A **literature/source note** says: *"This paper argues X, using method Y, and finds Z."*
It is *about the source*. It's tied to an author, a URL, a date. It summarises what *someone else* said. If the source disappeared, the note would lose its reason to exist.

A **permanent/base note** says: *"Concept X works because of Y. This connects to Z."*
It is *about the idea itself*. It's your synthesis — no single source owns it. It might draw from three papers, a video, and your own thinking. If every source disappeared, the note would still make sense.

**Example:**
- `02 Sources/Papers/de Ruiter et al. 2006.md` → literature note. "This paper found that turn-taking prediction relies on syntactic completion, not intonation."
- `05 Base Notes/Turn-Taking.md` → permanent note (if it existed). "Turn-taking in conversation is predicted primarily through syntax, with prosodic cues playing a secondary role. de Ruiter et al. 2006 showed this with... but Bogels & Torreira 2015 challenged it by..."

The source note *reports*. The base note *thinks*.

**Why other approaches blur this:**
- **PARA** doesn't distinguish — everything is a "note" filed by actionability. Good for project work, weak for long-term knowledge.
- **Second Brain** (Forte) focuses on *capturing* and *retrieving*, not on *synthesising*. You end up with lots of source notes and few permanent notes.
- **Zettelkasten** (Luhmann) is strict — literature notes are brief references, permanent notes are where the real work happens. The slip-box *is* the permanent notes.
- **This vault** is closest to Zettelkasten but pragmatic: source notes are richer than Luhmann's (full summaries, review questions) because they double as study material. Base notes are the synthesis layer.

**The test:** if you only have source notes and no base notes, you have a reference library, not a thinking tool. The pipeline isn't done until a fleeting note or source note has produced a base note or been consciously discarded.

### Building a Second Brain (Forte) — Deeper Look

Tiago Forte's *Building a Second Brain* (BASB) is the most popular modern PKM system. It is worth understanding in detail because it solves a real problem well, but stops short of where Zettelkasten starts.

**What it solves:**
Most people have information scattered across email, browser bookmarks, random docs, and sticky notes. BASB's core insight is that your brain is for *having* ideas, not *storing* them. The second brain is an external system that remembers things so your biological brain doesn't have to.

**The four components:**

*1. PARA (the organisational structure)*
Everything goes into one of four buckets based on how actionable it is:

| Bucket | Definition | Example |
|--------|-----------|---------|
| **Projects** | Has a goal and deadline | "Submit conference paper" |
| **Areas** | Ongoing responsibility, no end date | "Health", "Research", "Finance" |
| **Resources** | Topics of interest, for future reference | "Machine learning", "Journaling" |
| **Archives** | Inactive — completed projects, dropped areas | Old project folders |

The key principle: **organise by actionability, not by topic.** A note about nutrition goes under "Health" (an Area) if you actively manage your diet, or under "Resources/Nutrition" if it's just interesting. This makes retrieval purposeful — you look where the *work* is happening.

*2. CODE (the workflow)*
- **Capture** — save anything potentially useful (low bar, high volume)
- **Organise** — file it into PARA (quick, no deep thinking)
- **Distil** — highlight the most important parts (Progressive Summarisation)
- **Express** — use it to create something: a project, a paper, a decision

*3. Progressive Summarisation*
Forte's technique for making notes usable later. You layer highlights over time:
- Layer 1: Save the original note
- Layer 2: Bold the most important passages
- Layer 3: Highlight the most important of those bold passages
- Layer 4 (rare): Write an executive summary in your own words

The idea is that future-you can skim a note at whatever depth you need. A quick scan reads the highlights. A deep dive reads the whole thing.

*4. Intermediate Packets*
Break creative work into reusable chunks — outlines, drafts, summaries — stored as notes so they can be recombined into future projects. A literature summary written for one paper can be reused in the next.

**Where BASB falls short for research:**

BASB is optimised for *knowledge workers producing outputs* (reports, presentations, decisions). It is not optimised for *researchers building understanding*. The gap shows up in three places:

1. **Progressive Summarisation is not synthesis.** Highlighting what someone else said is curation, not thinking. You can perfectly summarise a paper without having understood how it connects to anything else you know. BASB gives you better source notes — it does not give you base notes.

2. **PARA files by project, not by concept.** If you learn something about neural networks while working on Project A, it goes in Project A's folder. When you start Project B on a related topic, that knowledge is inaccessible (or requires manual digging). Zettelkasten's concept-first filing means knowledge accumulates across projects.

3. **No explicit synthesis step.** CODE's "Express" step jumps from distilled notes to output. There is no intermediate step of building permanent concept notes that grow in value over time. The second brain gets bigger but not smarter.

**What BASB does better than Zettelkasten:**

- **Lower activation energy.** PARA is easier to set up and maintain than a Zettelkasten. Luhmann's slip-box requires discipline; PARA works even with messy habits.
- **Project focus keeps you shipping.** Filing by actionability means your notes directly support current work. A Zettelkasten can become an end in itself — beautifully organised but never producing anything.
- **Intermediate Packets are genuinely useful.** The idea that half-finished work is reusable is underrated. A draft outline is worth saving; most people throw it away.

**How this vault relates:**

This vault borrows from both:

| Element | Taken from |
|---------|-----------|
| `07 Projects/` structure | PARA — project-centric organisation |
| `08 Trackers/` task management | PARA — actionability focus |
| `02 Sources/` with summaries and review questions | BASB — rich literature notes, Progressive Summarisation |
| `05 Base Notes/` atomic concepts | Zettelkasten — permanent synthesis notes |
| `04 Indexes/` MOC pages | Zettelkasten — navigational index |
| Fleeting notes as temporary inbox | Zettelkasten — strict ephemerality |

The practical upshot: use BASB habits for *capturing and organising* (low friction, file quickly, highlight generously). Use Zettelkasten discipline for *processing* (the note isn't done until it has produced a base note or been consciously discarded).

---

## Task Management

Tasks are split by **time horizon**, not by life area. Each tracker file serves a different purpose.

### Tracker Files (`08 Trackers/`)

| File | Purpose | Changes how often |
|------|---------|-------------------|
| **Inbox.md** | Unsorted todos — landing zone from Telegram, pocket jot, quick capture | Daily (add), weekly (triage) |
| **This Week.md** | Max 10 items for the current week | Rebuilt every Sunday |
| **Deadlines.md** | Anything with a hard date, sorted chronologically | As needed |
| **Recurring.md** | Reference list of daily/weekly/monthly/quarterly tasks | Rarely — only when habits change |
| **Someday.md** | No-urgency backlog, grouped by life area | Monthly review |
| **Goals.md** | Yearly theme + quarterly goals (digital mirror of analogue journal) | Quarterly |
| **To Be Read.md** | Book reading list | As needed |
| **To Be Watched.md** | Film/show watchlist | As needed |
| **To Be Eaten.md** | Restaurants to try | As needed |
| **To Be Listened.md** | Music to listen to | As needed |

### Todo Routing

| Todo type | Where it lives | Why |
|-----------|---------------|-----|
| Quick "do today" | Life Tracker journal (analogue) | Handwritten = committed |
| Popped into your head | Pocket jot → Inbox.md on Sunday | Capture fast, process later |
| Has a deadline | Deadlines.md | Searchable, date-sorted |
| Work-specific | Work Obsidian vault | Separate context |
| "Someday/maybe" | Someday.md | No guilt parking lot |

### Weekly Review (Sunday, 20 min)

1. **Process pocket jot** — each item goes to Inbox.md, Life Tracker journal, or bin
2. **Triage Inbox.md** — move items to Deadlines, Someday, This Week, or delete
3. **Check Deadlines.md** — anything due this week?
4. **Check Goals.md** — what moves the needle?
5. **Rebuild This Week.md** — max 10 items, write a focus line

### Review Cadence

| When | What | Where |
|------|------|-------|
| **Morning** (5 min) | Intentions + habits | Life Tracker journal (analogue) |
| **Evening** (5 min) | Daily log + process pocket jot | Life Tracker journal (analogue) |
| **Sunday** (20 min) | Triage inbox, plan week | Both (analogue + Obsidian) |
| **1st of month** (30 min) | Review month, set next month goals, update deadlines | Both |
| **Quarterly** (1 hr) | Deep goal review, update Goals.md + analogue journal | Both |

---

## Analogue System

### Life Tracker Journal (A5, BuJo-inspired)

Uses a **Bullet Journal index** — first pages are a table of contents built as you go.

**Structure:**
```
Pages 1-4:    INDEX (topic → page numbers, built as you go)
Pages 5-8:    FUTURE LOG (6 months of key dates)
Pages 9-10:   YEARLY GOALS + IDENTITY STATEMENT
Pages 11-12:  QUARTERLY GOALS

Then flowing pages:
  → Monthly Log (calendar + task list)
  → Daily entries (3 intentions, habit row, evening log)
  → Collections as needed (e.g., "flat hunting", "gift ideas")
  → Next Monthly Log...
```

**Index example:**
```
INDEX
──────────────────────────────
Yearly Goals .............. 9
Q2 Goals ................. 11
April Monthly Log ........ 13
Habit Tracker - Apr ....... 15
Flat Hunting Notes .... 22, 47
Books Read 2026 .......... 34
May Monthly Log .......... 52
```

**BuJo rapid logging symbols:**
- `·` task
- `○` event
- `—` note
- `×` completed
- `>` migrated (moved to another day/month)
- `<` scheduled (moved to future log)

### Pocket Jot (Field Notes size)

- Always on you
- Write anything: todo, idea, thing to look up
- No organisation — just date each entry
- Process weekly on Sunday

---

## Daily Notes Workflow

Daily notes are **lightweight** — tasks and notes only. Journaling happens in the analogue Life Tracker.

### Template

```markdown
## {{date:dddd, MMMM Do, YYYY}}

### Tasks
- [ ]

### Notes

### Inbox (from pocket jot)
```

### During the Day

| Action | GUI | CLI |
|--------|-----|-----|
| Open daily note | Calendar plugin | `obsidian daily` |
| Add task | Type | `obsidian daily:append content="- [ ] Task"` |
| Check tasks | Open note | `obsidian tasks daily todo` |

### End of Day

Process captured items:
- **Tasks** → Keep or move to Inbox.md / project todo
- **Ideas** → Extract to fleeting note
- **Links** → Send to Telegram bot for source processing
- **Meeting notes** → Move to project folder

---

## Telegram Bot Routing

An external Telegram bot (or equivalent capture tool) handles incoming messages and routes them to the correct vault location. The example routing below is the convention this template assumes.

### Command Table

| Command | Destination |
|---------|-------------|
| `/todo <text>` | `08 Trackers/Inbox.md` |
| `/todo <text> @<date>` | `08 Trackers/Deadlines.md` (with parsed date) |
| `/someday <text>` | `08 Trackers/Someday.md` |
| `/read <url/text>` | `08 Trackers/To Be Read.md` |
| `/watch <url/text>` | `08 Trackers/To Be Watched.md` |
| `/note <text>` | `01 Fleeting Notes/<auto-title>.md` |
| `/daily <text>` | `06 Daily Notes/<today>.md` ### Notes |
| `/daily task <text>` | `06 Daily Notes/<today>.md` ### Tasks |
| `/project <name> todo <text>` | `07 Projects/<name>/Todo.md` |
| `/project <name> <text>` | `07 Projects/<name>/Notes.md` |
| plain text (no command) | `08 Trackers/Inbox.md` |
| bare URL (YouTube etc.) | `02 Sources/Videos/<Author – Title>.md` |
| bare URL (article/blog) | `02 Sources/Articles/<Title>.md` |
| `/note <url>` | `01 Fleeting Notes/<auto-title>.md` (raw, no AI summary) |

### Link Processing

When a bare URL is sent (no command prefix):
1. Detect type — YouTube/video platform → Videos, otherwise → Articles
2. Fetch metadata (title, author, published date)
3. Generate note using source template (frontmatter + AI summary)
4. Filename follows convention: Videos `Author – Title.md`, Articles `Title.md`

### Generated Note Structure

```markdown
---
title: "Article Title"
author: "[[Author Name]]"
source: "https://..."
tags: ["articles"]
---

> [!note]- Properties
> Status: #Inbox
> Tags: [[../04 Indexes/Topic|Topic]]

# Overview

## Summary
Brief overview + key bullet points.

## Action Items
- [ ] Actionable task

## Review Questions
1. Question for spaced repetition?

## Notes
```

### After Auto-Creation

1. Review generated note (status: #Inbox)
2. Add to relevant `04 Indexes/`
3. Create `05 Base Notes/` if ideas sparked
4. Change status to #Done

---

## Paper Reading Workflow

### Pipeline

```
To Read ──▶ Reading ──▶ Processing ──▶ Indexed
(backlog)   (fleeting)    (source)      (linked)
```

### Stage 1: Backlog

Track papers in `08 Trackers/To Be Read.md` or a project todo.

### Stage 2: Active Reading

Create a fleeting note for raw captures:

| GUI | CLI |
|-----|-----|
| `Ctrl+Shift+T` → Base template | `obsidian create path="01 Fleeting Notes/Reading - Author 2026.md" open` |

**Reading note structure:**
```markdown
# Reading: Author 2026 - Title

## First Pass (10 min)
- Paper type? Main claim? Context?

## Second Pass (1 hr)
- Key figures/tables
- Main arguments
- Questions

## Third Pass (deep)
- Methodology, criticisms, connections
```

### Stage 3: Process to Source

Convert to permanent source note using Paper template in `02 Sources/Papers/`.

### Stage 4: Index & Link

1. Add to relevant `04 Indexes/` MOC
2. Link to project if relevant
3. Create base notes for original insights

### Reading Depth by Paper Type

| Type | Depth | Time |
|------|-------|------|
| **Core** (directly relevant) | Full 3-pass | 3-4 hrs |
| **Supporting** (background) | 2-pass, key points | 1-2 hrs |
| **Survey** (overview) | Skim for references | 30 min |
| **Citation check** | Verify claims only | 15 min |

---

## Project Workflows

### Structure

```
07 Projects/
├── Project Name/
│   ├── Todo.md        ← project tasks
│   ├── Notes.md       ← running notes
│   └── Meeting Notes/
│       └── 2026-04-05.md
```

### CLI

```bash
# Add project task
obsidian append path="07 Projects/Project/Todo.md" content="\n- [ ] New task"

# Check project tasks
obsidian tasks path="07 Projects/Project" todo

# Create meeting note
obsidian create path="07 Projects/Project/Meeting Notes/2026-04-05.md" open
```

---

## Templates

| Template | Use For | Folder |
|----------|---------|--------|
| `Base` | Any new note, fleeting notes, base notes | Anywhere |
| `Paper` | Academic papers | `02 Sources/Papers/` |
| `Books` | Book notes | `02 Sources/Books/` |
| `Daily` | Daily notes | `06 Daily Notes/` |
| `Project` | New projects | `07 Projects/` |

---

## Quick Reference

| Action | GUI | CLI |
|--------|-----|-----|
| New note | `Ctrl+N` | `obsidian create name="Note" open` |
| From template | `Ctrl+Shift+T` | `obsidian create template=Base open` |
| Daily note | Calendar | `obsidian daily` |
| Add daily task | Type | `obsidian daily:append content="- [ ] Task"` |
| Search | `Ctrl+Shift+F` | `obsidian search query="term"` |
| Read file | Click | `obsidian read file=Name` |
| Toggle task | Checkbox | `obsidian task file=X line=N toggle` |
| Append | Edit | `obsidian append file=X content="text"` |

---

## See Also

- [[99 Templates/Base|Base Template]]
- [[99 Templates/Paper|Paper Template]]
- [[99 Templates/Books|Books Template]]
- [[04 Indexes/Turn-Taking|Example Index]]
- [[08 Trackers/Inbox|Inbox]]
- [[08 Trackers/This Week|This Week]]
- [[08 Trackers/Deadlines|Deadlines]]
- [[08 Trackers/Goals|Goals]]
- [[08 Trackers/To Be Read|Reading List]]
