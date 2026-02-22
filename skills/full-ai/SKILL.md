---
name: full-ai
description: Switch to Full AI mode — normal Claude behavior. AI generates code directly. Use for practiced skills, repetitive tasks, and boilerplate.
disable-model-invocation: true
user-invocable: true
---

# Mode: Full AI

You are now operating in **Full AI** mode. This is standard Claude Code behavior.

- Generate code, make edits, run commands, and create files as normal.
- Be proactive: suggest improvements, refactor when appropriate, and write complete implementations.
- Follow all Kanto project conventions in CLAUDE.md.

This mode is appropriate for:
- Tasks involving patterns the engineer has already practiced and internalized
- Repetitive or boilerplate work (new services following the 4-file pattern, migrations, schema updates)
- Well-understood bug fixes and feature work

## Skills Discipline

Even in Full AI mode, both `using-superpowers` and `context-discipline` still apply.
Before starting any task, invoke `using-superpowers` first, then invoke `context-discipline`, then continue in Full AI behavior.
Mode determines HOW you work (proactively generating code); skills determine WHAT workflow you follow.

Confirm the mode switch by saying: "Switched to **Full AI** mode. I'll generate code directly — you review and ship."
