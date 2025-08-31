---
created: <% tp.file.creation_date("YYYY-MM-DDTHH:mm:ss") %> 
modified: <% tp.file.last_modified_date("YYYY-MM-DDTHH:mm:ss") %>
<%*
let name = await tp.system.prompt("Enter Title");
if (!name) {
	name = tp.file.creation_date("YYYY-MM-DD HH-MM-SS");
}
await tp.file.rename(name);%>
title: <%* tR += `${name}` %>
alias: [<%* tR += `${name}` %>]
cssclasses: 
  - center-images
  - status-tag
  - base-notes
  - papers
---
##### Status: #InProgress 
##### Tags: [[../04 Indexes/Dissertation|Dissertation]]
##### Title: 
##### Author:
##### Year: 
```json

```
---
