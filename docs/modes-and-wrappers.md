# AI Modes and Superpowers Wrappers

This fork includes six mode-related skills under `skills/`:

- `full-ai`
- `learning`
- `manual`
- `full-ai-superpowers`
- `learning-superpowers`
- `manual-superpowers`

## Why This Is Fork-Safe

These additions are implemented as new skill folders only. Existing core Superpowers skills are not modified.

That keeps upstream sync straightforward:

1. `git fetch upstream`
2. `git merge upstream/main` (or your preferred sync-fork flow)

Because changes are additive, merge conflicts are less likely than if core files were heavily edited.

This fork automates the sync with a `git sync-main` alias (rebase onto upstream + `--force-with-lease` push). See [`syncing-the-fork.md`](syncing-the-fork.md) for what it does and how to set it up on a new machine.

## Codex and Cursor Installation Behavior

No extra installation steps are required beyond normal Superpowers install/update:

- Codex discovers skills from the installed Superpowers `skills/` directory.
- Cursor plugin metadata points to `./skills/`, so these mode skills are included automatically.

## Update Behavior for `*-superpowers` Wrappers

Wrapper skills call `using-superpowers` first, then the base mode skill.

This is a dynamic dependency:

- Updating `using-superpowers` updates wrapper behavior automatically.
- Reinstall is typically unnecessary; pulling latest changes and restarting the agent session is enough.
- Reinstall is only needed if install wiring is broken (for example, wrong clone path or broken symlink/plugin state).
