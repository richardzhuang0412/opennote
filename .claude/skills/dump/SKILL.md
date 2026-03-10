---
name: dump
description: Ultra-fast raw capture — minimal formatting, no embellishment
user_invocable: true
---

# /dump — Raw Capture

Capture the user's content as fast as possible with minimal processing.

## Instructions

1. Get the current date and time:
   ```
   TZ='TIMEZONE_PLACEHOLDER' date '+%Y-%m-%d %H:%M'
   ```
2. Determine a short topic slug from the content
3. Create `notes/YYYY-MM-DD_topic-slug.md` with this format:

```markdown
---
date: YYYY-MM-DD
created: "HH:MM"
type: note
summary: <one sentence max — just enough to identify the content later>
---

# <Short Title>

<user's content exactly as provided — no embellishment, no restructuring>
```

4. Commit and push:
   ```
   git add notes/YYYY-MM-DD_topic-slug.md
   git commit -m "note: <2-4 word summary>"
   git push
   ```

## Rules

- **No embellishment** — do not add context, analysis, or formatting beyond basic readability
- **No questions** — do not ask the user anything, just capture
- **Minimal summary** — one sentence max, keep it short
- **Preserve exact wording** — do not rephrase or restructure
- **Fast** — no unnecessary steps or output
