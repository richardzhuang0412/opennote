---
name: idea
description: Structured idea capture with potential and next steps
user_invocable: true
---

# /idea — Structured Idea Capture

Capture an idea with lightweight structure to make it actionable later.

## Instructions

1. Get the current date and time:
   ```
   TZ='TIMEZONE_PLACEHOLDER' date '+%Y-%m-%d %H:%M'
   ```
2. Determine a short topic slug from the idea
3. Create `notes/YYYY-MM-DD_topic-slug.md` with this format:

```markdown
---
date: YYYY-MM-DD
created: "HH:MM"
type: idea
summary: <1-2 sentence summary of the idea>
---

# <Idea Title>

<the idea, in the user's words — lightly formatted for readability>

## Potential

<2-3 bullet points on why this idea could be valuable, what it enables, or where it could lead>

## Next Steps

<2-3 concrete, small next actions to explore or validate this idea>
```

4. Commit and push:
   ```
   git add notes/YYYY-MM-DD_topic-slug.md
   git commit -m "idea: <2-4 word summary>"
   git push
   ```

## Rules

- Keep the user's original framing — don't over-polish
- **Potential** should be genuine observations, not hype
- **Next Steps** should be small and concrete — things that could be done in a day
- If the user provides context about why the idea matters, weave it in naturally
