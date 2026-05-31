<%*
let time = tp.date.now("YYYY-MM-DD")
-%>
---
title: PLAN
created: <% time %>
type: project-plan
visibility: private
status: active
---

# <% tp.file.folder() %> — Active Plan

The plan for in-flight work. Survives context loss so a later session can resume. When the work ships, fold the outcome into the latest `LOG.md` entry and clear this file. See [[Working with Claude]].

---

## Goal

*One or two sentences. What does "done" look like?*

## Context

*What forced this plan? Link to the `LOG.md` entry / `Notes.md` section / Base Note that motivates it.*

## Steps

- [ ] Step 1 — *files / area touched*
- [ ] Step 2
- [ ] Step 3

## Open decisions

- *Question* — *who decides / what to wait on*

## Out of scope

- *Things deliberately not in this plan, so they don't creep in.*

---

**Started:** <% time %>
**Status:** active
