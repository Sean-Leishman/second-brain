---
<%* 
let title = await tp.system.prompt("Enter title")
await tp.file.rename(title)
let status = "Inbox"
let time = tp.date.now("YYYY-MM-DD:HH-MM")

let imagePath = await tp.system.suggester(
  ["Browse for image", "Enter URL", "Skip"], 
  ["browse", "url", "skip"]
);

if (imagePath === "browse") {
  // This opens file browser
  let file = await tp.system.prompt("Drag image here or enter path");
  tr += `image: ${file}`
} else if (imagePath === "url") {
  let url = await tp.system.prompt("Enter image URL");
  tR += `image ${url}`;
}
%>
title: <% title %>
created: <% time %>
tags: book
links:
status: <% status %>
year:
author:
  - "{{author}}"
started: ""
finished: 
series:
series_part:
genres:
	- "{{category}}"
cssclasses: 
  - center-images
  - status-tag
  - books
---

> [!note]+ **Properties**
>  **Status:**
>  **Tags:**

--- 
![]({{coverUrl}})

# Annotation
> Annotate it all

# Characters

# Quotes
1. 

# Notes
> Notes is the key to remembering

