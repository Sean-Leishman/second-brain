<%*
let title = await tp.system.prompt("Enter title")
await tp.file.rename(title)
let time = tp.date.now("YYYY-MM-DD:HH-mm")
-%>
---
title: <% title %>
created: <% time %>
tags: movie
links:
status: Inbox
year:
director:
watched:
genres:
cssclasses:
  - center-images
  - status-tag
  - base-notes
---
> [!note]+ **Properties**
> **Created:** <% time %>
> **Status:** #Inbox
> **Tags:**
> **Director:**
> **Year:**
---
# Plot

# Characters

# Notes
