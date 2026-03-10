---
name: reflect
description: Periodic reflection that references recent notes and surfaces themes
user_invocable: true
---

# /reflect — Periodic Reflection

Create a reflection that draws on recent notes to surface themes and patterns.

## Instructions

1. Get the current date and time:
   ```
   TZ='TIMEZONE_PLACEHOLDER' date '+%Y-%m-%d %H:%M'
   ```
2. Scan recent notes using progressive exploration:
   - First, list files in `notes/` from the past 7 days (or the range the user specifies)
   - Read the frontmatter (first ~6 lines) of each to get summaries
   - Load full content of the most relevant notes
3. If the user provided a specific reflection prompt, use it as the lens. Otherwise, reflect broadly on what's been captured recently.
4. Create `notes/YYYY-MM-DD_reflection.md` with this format:

```markdown
---
date: YYYY-MM-DD
created: "HH:MM"
type: reflection
summary: <1-2 sentence summary of the reflection's key insight>
---

# Reflection — <Date or Period>

<the reflection — what stands out, what's changed, what's emerging>

## Themes

<3-5 recurring themes or patterns observed across recent notes, each as a bullet with a brief explanation>

## References

<list of note files referenced, as bullet points>
```

5. Commit and push:
   ```
   git add notes/YYYY-MM-DD_reflection.md
   git commit -m "reflect: <2-4 word summary>"
   git push
   ```

## Rules

- Ground the reflection in actual notes — don't fabricate themes
- Reference specific notes by filename so the reflection is traceable
- Keep it honest and useful, not generic or motivational
- If there are too few notes to reflect on, say so and capture what's there
