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

5. **Ask about reminders**: After capturing, ask the user if they want a scheduled reminder. For example:
   - "Want me to remind you about this tomorrow?"
   - "Want a daily reminder until Friday?"

6. **If the user wants a reminder**: Use `CronCreate` to schedule a follow-up that:
   - Reads the todo note to check its status
   - Reminds the user about the task
   - Example schedule: daily at 9 AM, or at a specific time the user requests

## Rules

- Always capture the task first, then offer the reminder
- Don't force reminders — only set them up if the user wants them
- Keep the note concise — this is a task, not an essay
- If the user provides a deadline, mention it in the reminder prompt
