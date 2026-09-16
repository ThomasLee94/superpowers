# Claude Code skill continuity

Follow the lifecycle below in Claude Code. For a durable recovery entry point,
merge the fenced section into the user's global `~/.claude/CLAUDE.md` during
authorized setup (use the configured `CLAUDE_CONFIG_DIR` when present).
Preserve existing rules and update an existing Skill Continuity section instead
of appending duplicates.

Superpowers' SessionStart hook supplies the using-superpowers bootstrap on
startup, resume, clear, and compaction. This reference tells the agent which
workflow state to restore; the agent must keep that state current during work.

```markdown
## Skill Continuity
- Maintain a persistent, session-specific record under `~/.claude/skill-state/` (or `$CLAUDE_CONFIG_DIR/skill-state/` when configured). Use the current session ID if the host provides it; do not assume a session-ID environment variable exists. Otherwise choose a unique record filename once and preserve that exact path in every handoff summary. Never infer the current record from the newest file or reuse another session's record.
- At the start of each user turn and after compaction or a resumed-session handoff, read the current session's record before substantive work. If no record is available, reconstruct one from current user instructions and context without inventing a previous mode or skill selection. A new session or `/clear` starts a separate record unless the user explicitly supplies a handoff.
- Record the active mode (or no selected mode), skill names and absolute installed `SKILL.md` paths, required dependencies/references, scope, user overrides, Ponytail level or opt-out, workflow stage, completed work, and next steps. Keep the record concise and free of secrets.
- Update the record when modes, skills, scope, or overrides change and at meaningful milestones. Persist changes during normal work instead of waiting for compaction.
- After compaction or a handoff, reload every applicable active skill with the Skill tool and read its required references before continuing. If a saved path is stale after a plugin update, resolve the same skill in the current installation and update the record. A note that a skill was previously loaded is not a substitute for its instructions.
- Preserve the current workflow stage and completed work. Do not restart completed steps or require the user to invoke the skills again.
- Keep task-wide skills active until the user changes them or their scope ends. Retire completed subtask skills. User instructions and overrides take precedence over skill guidance.
- Include the exact record path, active mode, skill names, and current workflow stage in every compaction/handoff summary you produce.
- Give subagents their applicable skill paths, mode, and overrides. Each writer uses its own record; subagents must not overwrite the parent record.
- After actually reading the enabled Ponytail policy on activation or post-compaction reload, emit exactly `Ponytail` on its own user-facing line. Do not emit it for a listing, summary, duplicate load, or while opted out.
```

These are recovery instructions, not a guarantee that every model response will
follow them. Do not create a record for an unrelated session during installation.
