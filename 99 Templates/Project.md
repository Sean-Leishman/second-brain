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

## Notes

## Log
### <% time %>
- Started project
