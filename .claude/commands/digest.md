---
description: Draft a weekly or monthly digest from Daily Notes + new Sources
argument-hint: [weekly|monthly]
---

Run the **Digest** workflow as defined in `CLAUDE.md` → *Personal Tracking → Digests*.

Period: $ARGUMENTS (default: weekly)

Steps:
1. Determine date range:
   - **weekly** → past 7 days from today
   - **monthly** → 1st of current month → today (or previous month if run on the 1st)
2. Scan in-range:
   - `06 Daily Notes/` for new entries
   - `02 Sources/` for new source notes
   - `01 Fleeting Notes/` for unprocessed captures
3. Create the digest file at `04 Indexes/Digests/<YYYY-WW>.md` (weekly) or `04 Indexes/Digests/<YYYY-MM>.md` (monthly), using `99 Templates/Digest.md` as the structure.
4. Fill in sections:
   - **Patterns** — recurring themes (3+ mentions or strong single signal)
   - **Anomalies** — outliers worth a second look
   - **Commitments made** — "I will / I want to / I'll try" statements; track follow-through next digest
   - **Contradictions with prior personal facts** — where this period's signal disagrees with `tag: personal` Base Notes; flag for `confidence` decay
   - **Candidate Base Notes** — topics with enough material to promote (title + Curate/Draft suggestion)
   - **Open threads** — questions raised, sources unread, ideas dropped mid-thought
5. Use **observational voice** — *"this week showed X"*, not *"you should do Y"*. I correct on review.
6. After I review: any accepted Candidate Base Notes kick off `/collate` or `/draft`. Append a `## [YYYY-MM-DD] digest | <period>` entry to `04 Indexes/Wiki Log.md`.

If the previous digest exists, link to it in the Log section of the new file.
