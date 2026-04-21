---
title: The Pipeline
date: 2026-04-21
tags:
  - pkm
  - building-in-public
  - cookonething
  - containsAI
---
# The Pipeline

Before you can publish anything, you need to know the pipe works.

Today I did the simplest possible thing: dropped a test file into a folder, typed three commands into a terminal, and watched a website update itself. No dashboard. No settings panel. No deploy button to click.

```
git add . 
git commit -m "test: verify publish pipeline" 
git push
```


That's it. GitHub tells Cloudflare something changed. Cloudflare builds the site. The file appears.

The second thing I did was create a symbolic link — a pointer from inside 
my Obsidian vault to the `content/` folder in the repository. In Windows, 
one PowerShell command does it:

New-Item -ItemType SymbolicLink -Path "path\to\vault\Garden" -Target "path\to\repo\content"

From that point on, the Garden folder inside Obsidian *is* the content folder 
in the repository. Not a copy. Not a sync. The same thing on disk, seen from 
two places at once.

Write a file in Obsidian. It appears in the repo. Push to GitHub. It's live.

There's no import step. No export step. No "remember to copy this across." 
The architecture removes the friction rather than managing it.

The pipeline isn't glamorous. But knowing it works changes something. The gap between "written" and "published" just collapsed to a git push.

That's what I'm cooking today.