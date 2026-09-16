# Codex skill continuity

Follow the lifecycle below while using Superpowers in Codex. To make its
recovery entry point durable, merge the fenced section into the user's global
`$CODEX_HOME/AGENTS.md` (`~/.codex/AGENTS.md` when `CODEX_HOME` is unset) as part
of an authorized setup. Preserve existing rules and update an existing Skill
Continuity section instead of appending duplicates.

Keep task records in the user's Codex directory, outside the plugin and source
repository. Record the actual installed skill paths on that machine. A record
identifies which instructions to restore; it does not replace those instructions.

```markdown
## Skill Continuity
- Maintain a task-specific record at `$CODEX_HOME/skill-state/<CODEX_THREAD_ID>.md`; use `~/.codex` when `CODEX_HOME` is unset. Obtain the task ID from the environment. If it is unavailable, choose a unique record path once and preserve it in every handoff summary. Never guess or reuse another task's record.
- At the start of each user turn and after context compaction or a handoff, read the current task's record before substantive work. Create a missing record from available user instructions and context; do not invent a previous mode or skill selection.
- Record the active mode (or no selected mode), active skill names and absolute `SKILL.md` paths, required dependencies/references, scope, user overrides, workflow stage, completed work, and next steps. Keep the record concise and free of secrets.
- Update the record when modes, skills, scope, or user overrides change and at meaningful milestones. Persist changes during normal work rather than waiting for compaction.
- After compaction or a handoff, re-read every applicable active skill and its required dependencies/references before continuing. Also re-read instructions whenever they are no longer available in context. A note that a skill was previously loaded is not sufficient.
- Restore the current workflow stage and preserve completed work. Do not restart completed steps or ask the user to invoke skills again.
- Keep task-wide skills active until the user changes them or their scope ends. Retire skills used only for completed subtasks. User instructions and overrides take precedence over skill guidance.
- Include the exact record path, active mode, active skill names, and current stage in every compaction/handoff summary you produce.
- Subagents sharing a task ID must not overwrite the parent's record. Give each writer a separate record with a stable agent-specific suffix and preserve its exact path in that agent's handoff.
```

These instructions automate recovery by directing the agent's behavior. They
are not a runtime hook and do not guarantee compliance through every compaction.
