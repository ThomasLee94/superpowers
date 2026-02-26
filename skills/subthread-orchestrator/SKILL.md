---
name: subthread-orchestrator
description: Use when you have 2+ independent implementation tasks with minimal shared state and want the parent thread to keep context clean by dispatching scoped subthreads with mandatory review gates.
---

# Subthread Orchestrator

## Overview

Keep the parent thread focused on orchestration while subthreads execute narrow implementation scopes.

**Core principle:** Parent thread plans and integrates. Subthreads implement and review.

## When to Use

Use this skill when all are true:
- You have 2+ independent tasks.
- Tasks can run without shared mutable state.
- Parent context is getting noisy or likely to bloat.

Do not use when:
- Tasks are tightly coupled.
- Multiple tasks need to edit the same file/function concurrently.
- Order dependencies are unclear.

## Orchestration Workflow

1. **Independence Check**
- Confirm each task has isolated scope.
- If tasks are coupled, run sequentially in parent thread instead.

2. **Create Dispatch Brief**
- Write a short brief per task with:
  - goal
  - exact scope (files/functions)
  - constraints
  - acceptance criteria
  - required verification command

3. **Dispatch Subthreads**
- Dispatch one subthread per task (max 3 active).
- Each subthread must:
  - invoke `using-superpowers`
  - invoke the task-specific implementation skill (for example a builder skill or mode skill)
  - invoke `requesting-code-review` before returning results

4. **Review Gate (Hard)**
- Subthread output is not accepted until:
  - Critical review issues are fixed
  - Important review issues are fixed or explicitly approved by engineer

5. **Integrate in Parent**
- Parent thread merges accepted outputs.
- Run aggregate verification across integrated changes.
- Summarize what changed, open risks, and next actions.

## Subthread Output Contract

Each subthread must return:
- files changed
- summary of implementation
- verification commands run + outcomes
- review findings status (open/closed)
- unresolved questions/risks

If contract is incomplete, send subthread back to finish.

## Guardrails

- Max 3 active subthreads.
- One task domain per subthread.
- No broad context dump to subthreads; pass only task-relevant brief.
- If cross-task dependency appears, stop parallel dispatch and switch to sequential integration.

