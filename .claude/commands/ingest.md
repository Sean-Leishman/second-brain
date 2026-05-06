---
description: Integrate a source note into the wiki layer (Base Notes, Indexes, Log)
argument-hint: [source-note path or URL]
---

Run the **Ingest** operation as defined in `CLAUDE.md`.

Target: $ARGUMENTS

Steps:
1. Read the source note (already-summarised by the bot or template). If $ARGUMENTS is a raw URL/PDF, write the source note first using the appropriate template — but flag that the bot is the preferred path.
2. Discuss takeaways with me before writing anything load-bearing. Surface contradictions with prior wiki claims, candidates for new Base Notes, and extensions to existing ones.
3. Update relevant Base Notes in `05 Base Notes/`. **Propose new Base Notes; do not create silently.** Default to Curate mode for personal topics, Draft mode for technical synthesis (ask if unclear).
4. Maintain `sources:` provenance — append this source to the frontmatter of every Base Note that absorbs material from it.
5. Update `04 Indexes/Wiki Index.md` and any topic MOC affected.
6. Flip the source note's status from `#Inbox` to `#Done`.
7. Append a `## [YYYY-MM-DD] ingest | <source title>` entry to `04 Indexes/Wiki Log.md`.

If multiple sources are queued, do them one at a time with me in the loop unless I explicitly say batch.
