# AI Modes and Superpowers Wrappers

This fork includes eight mode-related skills under `skills/`:

- `full-ai`
- `learning`
- `manual`
- `guided-full-ai`
- `full-ai-superpowers`
- `learning-superpowers`
- `manual-superpowers`
- `guided-full-ai-superpowers`

## Why This Is Fork-Safe

The modes and wrappers live in their own skill folders. Every skill also links to [the shared Ponytail policy](../skills/using-superpowers/references/ponytail.md), so simplicity applies to direct invocations as well as the `using-superpowers` bootstrap. Learning, Manual, and Guided mode restrictions still control what the agent may do.

That keeps upstream sync straightforward:

1. `git fetch upstream`
2. `git merge upstream/main` (or your preferred sync-fork flow)

When resolving upstream conflicts, preserve the small policy links and add the same link to any new skill. The policy itself is maintained in one reference file.

This fork automates the sync with a `git sync-main` alias (rebase onto upstream + `--force-with-lease` push). See [`syncing-the-fork.md`](syncing-the-fork.md) for what it does and how to set it up on a new machine.

## Codex and Cursor Installation Behavior

No extra installation steps are required beyond normal Superpowers install/update:

- Codex discovers skills from the installed Superpowers `skills/` directory.
- Cursor plugin metadata points to `./skills/`, so these mode skills are included automatically.

## Update Behavior for `*-superpowers` Wrappers

Wrapper skills call `using-superpowers` first, then `context-discipline`, then the base mode skill. The shared policy does not change this order.

This is a dynamic dependency:

- Updating `using-superpowers` updates wrapper behavior automatically.
- Reinstall is typically unnecessary; pulling latest changes and restarting the agent session is enough.
- Reinstall is only needed if install wiring is broken (for example, wrong clone path or broken symlink/plugin state).
