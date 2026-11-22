---
title: Home
created: 2026-11-22
type: index
cssclasses:
  - home
---
# Home

[[Current WIP]] · [[Goals]] · [[Review Queue.base|Review Queue]] · [[00 Vault Guide|Vault Guide]]

> [!board]
> > [!todo] This Week
> > ```dataview
> > TASK FROM "08 Trackers/This Week" WHERE !completed
> > ```
>
> > [!inbox] Inbox
> > ```dataview
> > TASK FROM "08 Trackers/Inbox" WHERE !completed
> > ```
>
> > [!deadline] Deadlines
> > ```dataview
> > TASK FROM "08 Trackers/Deadlines" WHERE !completed SORT text ASC
> > ```
>
> > [!someday] Someday
> > ```dataview
> > TASK FROM "08 Trackers/Someday" WHERE !completed GROUP BY section
> > ```
