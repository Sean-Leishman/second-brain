<%*
let time = tp.date.now("YYYY-MM-DD")
-%>
---
title: DECISIONS
created: <% time %>
type: project-decisions
visibility: private
---

# <% tp.file.folder() %> — Decisions

Load-bearing decisions only (shapes architecture, will be questioned later, expensive to
reverse). Newest first. Never delete a superseded decision — change its **Status**. Each
decision carries a stable `D-NNN` id, a concrete **Referent** (how it's retrieved), and the
**Constraint** it implies (the do/don't rule to check before editing the referent). See
[[Working with Claude]].

---

<!-- Copy this block per decision (newest at top):

### D-001 — <short title>
- **Status:** accepted          ⟨accepted | superseded by D-NNN | revisited⟩
- **Referent:** `crate/path/**` · `module::symbol` · `subsystem`
- **Context:** what forced the choice
- **Decision:** what was chosen
- **Why:** alternatives rejected and the reason
- **Constraint:** the imperative this establishes (e.g. "don't add a second eviction path")

-->
