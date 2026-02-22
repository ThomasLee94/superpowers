---
name: context-discipline
description: Use when a conversation is becoming long or unfocused, when switching between unrelated tasks mid-session, or before starting a complex multi-step task that needs scoping
---

# Context Discipline

## Overview

Long AI sessions degrade. Context fills up, compaction loses nuance, tangent requests pollute working memory. Combat this by scoping sessions, externalizing state to files, and detecting topic drift.

**Core principle:** Sessions are disposable. Files are durable. Important context belongs in files, not chat history.

## Passive Behaviors (Apply Throughout Any Session)

### Detect Tangent Requests

When a user request is **unrelated to the current task**, flag it before executing:

> "This looks like a separate topic from [current work]. I can handle it here, but it'll add noise to our context. Want me to proceed, or would you prefer a fresh thread?"

**Tangent = different feature, file, subsystem, or unrelated config/tooling question.**
**NOT a tangent = clarifying questions, related refactoring, reviewing what was just built.**

### Externalize After Milestones

After completing significant work (feature implemented, bug fixed, architecture decided), proactively write a brief progress note to `docs/progress/`.

**File naming:** `YYYY-MM-DD-<topic>-<platform>.md`

- Platforms: `cursor`, `claude-code`, `codex`
- Example: `2026-02-21-auth-refactor-cursor.md`

**Contents:**

- **Date**
- **Platform:** which tool produced this
- **Status:** what's done
- **Decisions:** key choices made and why
- **Next:** what remains

### Suggest Splitting Long Sessions

After 15+ back-and-forth exchanges on implementation work, suggest:

> "We've covered a lot of ground. If quality matters for the next piece, a fresh thread with a handoff file would give better results."

## Intentional Session Scoping

### Before a Big Task

Break work into focused phases. Each phase = one session:

| Phase | Scope | Output |
|-------|-------|--------|
| Architecture | Design decisions, component boundaries | Design doc |
| Implementation | Build one feature/component | Working code + tests |
| Review | Verify against requirements | Issues list |
| Debug | Fix specific issues | Fixes + root cause notes |

**Don't mix phases.** "Build this feature and also debug that other thing" guarantees both get done poorly.

### Starting a Scoped Session

1. State the single goal for this session
2. List what files/context is needed
3. Note what is explicitly OUT of scope
4. Do the work
5. Externalize results before ending

### Handing Off Between Sessions

Write a handoff file to `docs/progress/YYYY-MM-DD-<topic>-<platform>.md` that a fresh session can consume:

- **Goal:** what we're building
- **Platform:** which tool produced this (`cursor`, `claude-code`, `codex`)
- **Done:** completed work, with file paths
- **Current state:** what works, what doesn't
- **Next steps:** specific remaining tasks
- **Key decisions:** choices made, with reasoning
- **Out of scope:** explicitly deferred items

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| "Just one quick question" mid-task | Open new thread |
| No progress notes after major work | Write handoff before moving on |
| Mixing debug + feature + refactor | One session, one purpose |
| Restarting without handoff file | Always externalize before ending |
| Ignoring context length | Suggest split after 15+ exchanges |

## Cursor Rule Companion

For always-on passive behavior in Cursor, copy `cursor-rule.mdc` from this skill directory to your project's `.cursor/rules/context-hygiene.mdc`.
