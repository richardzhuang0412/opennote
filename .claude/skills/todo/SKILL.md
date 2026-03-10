---
name: todo
description: Task capture with optional scheduled follow-up reminders
user_invocable: true
---

# /todo — Task Capture

Capture a task as a note and optionally schedule a follow-up reminder.

## Instructions

1. Get the current date and time:
   ```
   TZ='TIMEZONE_PLACEHOLDER' date '+%Y-%m-%d %H:%M'
   ```
2. Parse the user's input for:
   - The task description
   - Priority (if mentioned — high/medium/low, default: medium)
   - Deadline (if mentioned — extract the date)
   - Reminder time (if mentioned — e.g., "in 10 minutes", "tomorrow at 9am")
3. Create `notes/YYYY-MM-DD_todo-slug.md` with this format:

```markdown
---
date: YYYY-MM-DD
created: "HH:MM"
type: todo
summary: <1 sentence describing the task>
priority: <high|medium|low>
deadline: <YYYY-MM-DD if given, otherwise omit this field>
status: open
---

# TODO: <Task Title>

<task description in the user's words>
```

4. Commit and push:
   ```
   git add notes/YYYY-MM-DD_todo-slug.md
   git commit -m "todo: <2-4 word summary>"
   git push
   ```

5. **Schedule a reminder if requested**: If the user specified a reminder time (e.g., "in 10 minutes", "remind me at 3pm", "remind me tomorrow"), schedule a macOS desktop notification using a background process:

   ```bash
   # Calculate seconds until reminder
   # For relative times like "in 10 minutes": SECONDS=600
   # For absolute times: compute seconds from now until that time
   nohup bash -c 'sleep <SECONDS> && osascript <<APPLESCRIPT
   display notification "<task summary>" with title "📓 OpenNote" subtitle "Todo Reminder" sound name "Ping"
   APPLESCRIPT' > /dev/null 2>&1 &
   ```

   **Important**: Always use a heredoc (`<<APPLESCRIPT ... APPLESCRIPT`) to pass the script to `osascript` — do NOT use `osascript -e` with inline quotes, as emoji and special characters cause parsing errors.

   - Parse natural language times: "in 10 minutes" = 600s, "in 1 hour" = 3600s, "tomorrow at 9am" = seconds until then
   - For absolute times, calculate seconds using: `$(( $(TZ='TIMEZONE_PLACEHOLDER' date -j -f '%Y-%m-%d %H:%M' 'TARGET_DATETIME' '+%s') - $(date '+%s') ))`
   - Tell the user the exact time the reminder will fire

6. **If no reminder was mentioned**: Ask the user if they want one. For example:
   - "Want me to remind you about this in an hour?"
   - If the user declines or doesn't respond, that's fine — the task is already captured.

## Terminal mode warning

**Important**: If the user is running this via `claude -p` (one-shot terminal mode, e.g., `note "/todo ..."` via a shell alias), warn them:

> "⚠️ You're in terminal mode. The reminder will only fire if this terminal window stays open. For reliable reminders, keep the window open or run `/todo` inside an interactive `claude` session."

When in doubt, include the warning.

## Rules

- Always capture the task first, then handle the reminder
- Don't force reminders — only set them up if the user wants them
- Keep the note concise — this is a task, not an essay
- If the user provides a deadline, mention it in the reminder prompt
- Use `osascript` with heredoc for notifications — works natively on macOS, no extra dependencies
