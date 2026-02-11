<%*
let title = await tp.system.prompt("Enter title")
await tp.file.rename(title)
let time = tp.date.now("YYYY-MM-DD:HH-mm")
-%>
---
title: <% title %>
created: <% time %>
links:
tags:
source:
cssclasses:
  - center-images
  - status-tag
  - base-notes
---
> [!note]+ **Properties**
> **Created:** <% time %>
> **Origin:**
> **Status:** #Inbox
> **Tags:**
---
