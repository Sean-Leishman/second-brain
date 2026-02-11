<%*
let title = await tp.system.prompt("Enter title")
if (!title) {
	title = tp.file.creation_date("YYYY-MM-DD HH-mm-ss");
}
await tp.file.rename(title)
let time = tp.date.now("YYYY-MM-DD:HH-mm")
-%>
---
title: <% title %>
created: <% time %>
author:
year:
doi:
links:
tags: paper
cssclasses:
  - center-images
  - status-tag
  - base-notes
---
> [!note]+ **Properties**
> **Created:** <% time %>
> **Status:** #Inbox
> **Tags:** [[../04 Indexes/Dissertation|Dissertation]]
> **Author:**
> **Year:**
> **DOI:**
---
# Abstract

# Key Contributions

# Methodology

# Results

# Notes
