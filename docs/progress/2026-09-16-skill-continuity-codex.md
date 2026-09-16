# Codex and Claude Code skill continuity

- Date: 2026-09-16
- Platform: Codex
- Goal: Restore active skills after compaction without repeated user invocation.
- Status: Added a reusable Codex reference and global `AGENTS.md` setup block, linked from the Codex bootstrap reference, context-discipline skill, and README. Added a one-word Ponytail acknowledgment after activation and post-compaction reloads.
- Decisions: Store task records outside the repository and plugin. Preserve mode, scope, overrides, workflow stage, and installed skill paths. Reload applicable instructions after compaction; retire completed subtask skills. Separate records for agents that share a task ID.
- Validation: Reviewed the diff, checked local continuity-reference links, and ran `git diff --check` successfully. This documentation change does not exercise a live compaction cycle.
- Installation: Synced all 24 skills (65 source files) to the shared installation and verified exact source-file matches and the discovery symlink.
- Delivery: User requested committing these changes, pushing to the configured origin, and syncing the installed checkout. No marketplace publication is part of this task.

## Claude Code continuation

- Added a Claude continuity reference, global `CLAUDE.md` setup guidance, and bootstrap/context-discipline links. Includes per-session records, skill reloads, Ponytail state and acknowledgment, stale plugin-path recovery, and separate subagent records.
- Extended SessionStart registration to resumed sessions as well as startup, clear, and compaction.
- Corrected installation guidance: Claude uses a separate marketplace plugin cache rather than the shared Codex checkout.
- Validation: The new resume-trigger assertion failed before the matcher change and passed afterward; all six hook checks pass. Shell syntax, continuity links, diff whitespace, and marketplace/plugin manifests pass validation. The plugin validator warns that the pre-existing contributor `CLAUDE.md` is not plugin context; recovery ships through skills and user-level `CLAUDE.md`.
- Deployment: Install the updated customized fork and retain only that Superpowers distribution enabled. A live model compaction cycle has not been exercised.
