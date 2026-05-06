---
description: Health-check the wiki — contradictions, orphans, broken links, stale claims
---

Run the **Lint** operation as defined in `CLAUDE.md`.

Scan and report:
- **Contradictions** between Base Notes (especially personal facts that may have been superseded).
- **Stale claims** — sources that have since been challenged by newer ingests.
- **Orphan pages** — Base Notes with no inbound links.
- **Missing concepts** — terms repeatedly referenced in Sources/Daily Notes without a Base Note.
- **Missing cross-references** — Base Notes that should link to each other but don't.
- **Broken links** in `04 Indexes/Wiki Index.md` and topic MOCs.
- **Frontmatter drift** — Base Notes missing `sources:`, personal Base Notes missing `confidence:`, anything missing `tags`/`visibility`.

Output a punch list — *what, why, which files, suggested action*. **No file writes during the proposal phase.** I pick what to act on.

Append a `## [YYYY-MM-DD] lint | <summary>` entry to `04 Indexes/Wiki Log.md` after the punch list is produced.
