---
description: Wiki-wide structural pass — propose merges, splits, new MOCs, regenerate Wiki Map
argument-hint: [scope, e.g. "personal", "distributed-systems", or empty for full]
---

Run the **Reindex** operation as defined in `CLAUDE.md`.

Scope: $ARGUMENTS (default: all of `05 Base Notes/` + `04 Indexes/`)

Steps:
1. Scan in-scope Base Notes and Indexes.
2. Cluster by topic — group notes sharing concepts, citations, or tags. Surface unexpected clusters.
3. Propose:
   - **New MOC pages** when a cluster has 3+ Base Notes and no existing index.
   - **Merge candidates** — pairs of Base Notes that have drifted into the same concept.
   - **Split candidates** — single Base Notes covering two distinct ideas.
   - **Re-tagging** — notes whose tags don't match content, or missing tags.
   - **Index updates** — `04 Indexes/Wiki Index.md` entries to add/remove/rewrite.
   - **Map updates** — regenerate `04 Indexes/Wiki Map.md` with current density per domain and gaps.
   - **Orphan adoption** — orphaned notes that fit existing MOCs.
   - **Decaying confidence** — personal Base Notes with no reinforcing signal in 8+ weeks.
   - **Cross-project promotions** — concepts repeated across 2+ projects in `07 Projects/` with no Base Note.
4. Output a punch list. Each item: *what, why, which files, Curate or Draft mode if authoring is involved*.
5. **No file writes during proposal phase.** I pick what to act on; you execute one at a time with diffs.
6. Append a `## [YYYY-MM-DD] reindex | <summary>` entry to `04 Indexes/Wiki Log.md` summarising proposed and accepted items.
