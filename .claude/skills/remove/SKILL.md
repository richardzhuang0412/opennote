---
name: remove
description: Find and remove a previous note that's no longer needed
user_invocable: true
---

# /remove — Remove a Note

Find and delete a note that's outdated, wrong, or no longer needed.

## Instructions

**Batch operations. Minimize tool calls.**

1. Search for matching notes in one Bash call:

   ```bash
   grep -rl "<keyword>" notes/ && echo "---" && ls -1 notes/ | grep -i "<keyword>"
   ```

   Use both content search and filename search to find candidates.

2. Show the user a short list of matches with their summaries (read frontmatter):

   ```bash
   head -6 notes/<match1>.md notes/<match2>.md
   ```

3. **Ask the user to confirm** which note(s) to delete. Never delete without confirmation.

4. Once confirmed, delete + commit + push in one call:

   ```bash
   rm notes/<filename>.md && \
   git add -A && git commit -m "remove: <brief reason>" && git push &
   ```

## Rules

- **Always confirm before deleting** — show the note title and summary first
- If multiple matches, list them and let the user pick
- If no matches found, say so and suggest alternative search terms
- Keep output concise — just filenames and summaries, not full content
