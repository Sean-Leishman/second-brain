<%*
let time = tp.date.now("YYYY-MM-DD")
-%>
---
title: LOG
created: <% time %>
type: project-log
visibility: private
---

# <% tp.file.folder() %> — Session Log

Append-only. Newest first. One entry per working session. See [[Working with Claude]] for the convention.

---

## [<% time %>] — <session title>

**What changed**
- 

**Decisions**
- **D-NNN** (`referent`) — *what was decided* — *why*. Promote to `DECISIONS.md` if load-bearing.

**Learnings / insights**
- 

**Open / next**
- 
