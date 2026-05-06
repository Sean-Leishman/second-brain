<%*
let period = await tp.system.suggester(["weekly", "monthly"], ["weekly", "monthly"], false, "Digest period")
let title
if (period === "weekly") {
  title = tp.date.now("GGGG-[W]WW")
} else {
  title = tp.date.now("YYYY-MM")
}
await tp.file.rename(title)
let time = tp.date.now("YYYY-MM-DD:HH-mm")
-%>
---
title: <% title %>
created: <% time %>
type: digest
period: <% period %>
visibility: private
tags:
  - digest
  - <% period %>
cssclasses:
  - base-notes
---
> [!note]+ **Digest — <% title %> (<% period %>)**
> **Range:** <% period === "weekly" ? tp.date.now("YYYY-MM-DD", "-6d") : tp.date.now("YYYY-MM-01") %> → <% tp.date.now("YYYY-MM-DD") %>
> **Sources scanned:** Daily Notes, new Sources, new Fleeting Notes
> **Author:** agent draft (user reviews)

---
## Patterns
*Recurring themes across the period. 3+ mentions or strong single signal.*

## Anomalies
*Things that broke the pattern — outliers worth a second look.*

## Commitments made
*"I will / I want to / I'll try" statements from Daily Notes. Track follow-through next digest.*

## Contradictions with prior personal facts
*Where this period's signal disagrees with `tag: personal` Base Notes. Trust the present; flag the fact for update.*

## Candidate Base Notes
*Topics that have accumulated enough material to promote. Format: title — what to collate — Curate or Draft mode suggestion.*

## Open threads
*Questions raised but unanswered, sources flagged but unread, ideas dropped mid-thought.*

## Log
- Sources counted:
- Daily Notes scanned:
- Prior digest: [[]]
