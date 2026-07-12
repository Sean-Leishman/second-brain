<%*
let time = tp.date.now("YYYY-MM-DD:HH-mm")
-%>
---
title: <% tp.file.title %>
created: <% time %>
visibility: private
summary: ""
links:
tags:
  - Unfiled
sources:
cssclasses:
  - center-images
  - status-tag
  - base-notes
---
> [!note]+ **Properties**
> **Created:** <% time %>
> **Origin:**
> **Status:** #Unfiled
> **Tags:**
---

%% Just write. No prompt, no naming decision, no metadata — start typing.
Leave every blank above empty: summary, tags, links, sources, Origin are the agent's job, not yours.
Don't bother naming the file either; rename it whenever, or never.

When you're done (or not), tell Claude **"file this"**: it names the note if it's still Untitled, syncs
the title, fills the frontmatter, cross-links, indexes, logs, and removes #Unfiled.
Delete this comment whenever. The #Unfiled tag is what puts the note in the queue — see 08 Trackers/Unfiled.base %%

