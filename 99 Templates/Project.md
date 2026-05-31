<%*
let title = await tp.system.prompt("Enter project name")
await tp.file.rename(title)
let time = tp.date.now("YYYY-MM-DD:HH-mm")
-%>
---
title: <% title %>
created: <% time %>
links:
tags: project
status: Active
cssclasses:
  - center-images
  - status-tag
  - base-notes
---
> [!note]+ **Properties**
> **Created:** <% time %>
> **Origin:**
> **Status:** #Working
> **Tags:**
---
## Overview

## Goals
- [ ] Goal 1
- [ ] Goal 2

## Tasks
- [ ] Task 1
- [ ] Task 2

## Decisions

*Load-bearing decisions live in `DECISIONS.md` at the project root (id + referent + the constraint each implies). This section keeps only a pointer; day-to-day choices stay in `LOG.md`. See [[Working with Claude]].*

## Notes

---

This file is the project's `Notes.md` — the living overview. Session-by-session work goes in a sibling `LOG.md` (Project LOG template) and in-flight plans go in `PLAN.md` (Project PLAN template).
