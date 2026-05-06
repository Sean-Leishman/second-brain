---
description: Ask a question against the wiki (with Open Questions logging)
argument-hint: <question>
---

Run the **Query** operation as defined in `CLAUDE.md`.

Question: $ARGUMENTS

Steps:
1. Read `04 Indexes/Wiki Index.md` first; pick relevant pages from the catalog.
2. Read those pages. If insufficient, fall back to grep across `05 Base Notes/`, then `02 Sources/`, then raw layers.
3. Synthesise an answer with `[[wikilinks]]` for every citation.
4. **If the answer is non-trivial and reusable** (a comparison, an analysis, a connection), offer to file it back as a new Base Note or MOC entry.
5. **If the wiki could not fully answer**, append the question to `04 Indexes/Open Questions.md`. Format:
   ```
   ## [YYYY-MM-DD] <question>
   - **Gap:** missing-source | missing-base-note | unresolved-contradiction | out-of-scope
   - **Suggested action:** <ingest X | write Base Note on Y | lint contradiction A vs B>
   - **Related:** [[links]]
   - **Status:** open
   ```
   This is non-optional — Open Questions is the research backlog.
6. Append to `04 Indexes/Wiki Log.md` only if the query produced new wiki content (Base Note, MOC entry, or Open Questions entry).
