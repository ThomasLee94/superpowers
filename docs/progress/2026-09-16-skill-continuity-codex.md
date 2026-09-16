# Codex skill continuity

- Date: 2026-09-16
- Platform: Codex
- Goal: Restore active skills after compaction without repeated user invocation.
- Status: Added a reusable Codex reference and global `AGENTS.md` setup block, linked from the Codex bootstrap reference, context-discipline skill, and README. Added a one-word Ponytail acknowledgment after activation and post-compaction reloads.
- Decisions: Store task records outside the repository and plugin. Preserve mode, scope, overrides, workflow stage, and installed skill paths. Reload applicable instructions after compaction; retire completed subtask skills. Separate records for agents that share a task ID.
- Validation: Reviewed the diff, checked local continuity-reference links, and ran `git diff --check` successfully. This documentation change does not exercise a live compaction cycle.
- Installation: Synced all 24 skills (65 source files) to the shared installation and verified exact source-file matches and the discovery symlink.
- Delivery: User requested committing these changes, pushing to the configured origin, and syncing the installed checkout. No marketplace publication is part of this task.
