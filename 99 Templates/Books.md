<%*
let title = await tp.system.prompt("Enter title")
await tp.file.rename(title)
let time = tp.date.now("YYYY-MM-DD:HH-mm")
-%>
---
title: <% title %>
created: <% time %>
tags: book
links:
status: Inbox
year:
author:
started:
finished:
series:
series_part:
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
> **Author:**
> **Year:**
---
# Annotation

# Characters

# Quotes

# Notes
