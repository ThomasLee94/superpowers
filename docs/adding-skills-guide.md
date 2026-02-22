# Adding a New Skill to Superpowers

Guide for creating a new skill and deploying it across Cursor, Codex, and Claude Code — including wiring it into the three modes (Full AI, Learning, Manual).

## 1. Create the Skill

```
skills/<skill-name>/
  SKILL.md              # Required
  cursor-rule.mdc       # Optional — always-on Cursor rule companion
  supporting-files.*    # Optional — reference docs, scripts
```

Follow `skills/writing-skills/SKILL.md` for content guidelines. Key constraints:

- YAML frontmatter: `name` and `description` only (max 1024 chars)
- Description starts with "Use when..." — triggering conditions only, no workflow summary
- Under 500 words

## 2. Wire Into Modes (If Skill Should Always Apply)

If the skill should be active regardless of mode (like `using-superpowers` or `context-discipline`), update three places:

### a. Each base mode's "Skills Discipline" section

Update `skills/full-ai/SKILL.md`, `skills/learning/SKILL.md`, and `skills/manual/SKILL.md`:

```markdown
## Skills Discipline

Even in [Mode] mode, `using-superpowers`, `context-discipline`, and `<new-skill>` still apply.
Before starting any task, invoke `using-superpowers` first, then invoke `context-discipline`,
then invoke `<new-skill>`, then continue in [Mode] behavior.
```

### b. Each wrapper's invocation order

Update `skills/full-ai-superpowers/SKILL.md`, `skills/learning-superpowers/SKILL.md`, and `skills/manual-superpowers/SKILL.md`:

```markdown
## Required Invocation Order

1. Invoke `using-superpowers` first and follow it.
2. Then invoke `context-discipline` and follow it.
3. Then invoke `<new-skill>` and follow it.
4. Then invoke `full-ai` and follow it.
```

### c. Skip this step if the skill is situational

Skills that only fire when matched (like `systematic-debugging` or `test-driven-development`) don't need mode wiring — they're invoked by the skill system when relevant.

## 3. Deploy the Cursor Rule Companion (If Applicable)

If the skill has a `cursor-rule.mdc` for passive always-on behavior in Cursor, copy it to each project:

```bash
cp skills/<skill-name>/cursor-rule.mdc ~/Desktop/Code/kanto/.cursor/rules/<skill-name>.mdc
cp skills/<skill-name>/cursor-rule.mdc ~/Desktop/Code/admin-portal/.cursor/rules/<skill-name>.mdc
cp skills/<skill-name>/cursor-rule.mdc ~/Desktop/Code/nclusion-mobile-app/.cursor/rules/<skill-name>.mdc
```

Cursor rules are project-scoped. There is no global rules directory — each project needs its own copy.

## 4. Commit and Push

```bash
cd ~/Desktop/Code/superpowers
git add skills/<skill-name>/ skills/full-ai/ skills/learning/ skills/manual/ \
        skills/full-ai-superpowers/ skills/learning-superpowers/ skills/manual-superpowers/
git commit -m "add <skill-name> skill and wire into modes"
git push origin main
```

## 5. Install Across Platforms

### Codex & Claude Code (shared installation)

Both read from `~/.codex/superpowers/skills/` (Codex via symlink, Claude Code via plugin).

```bash
cd ~/.codex/superpowers
git pull origin main
```

Restart the agent session. New skills are discovered on startup.

### Cursor

Cursor picks up skills from the same `~/.codex/superpowers/skills/` path via the `~/.agents/skills/superpowers` symlink. The `git pull` above covers it.

Restart Cursor or start a new chat session.

**For the Cursor rule companion**, you must separately copy the `.mdc` file to each project (step 3 above). This is the one extra step Cursor requires that Codex and Claude Code don't.

## Platform Differences Summary

| Aspect | Cursor | Codex | Claude Code |
|--------|--------|-------|-------------|
| **Skill discovery** | Available skills list (via hooks + symlink) | Scans `~/.agents/skills/` at startup | Plugin system (`.claude-plugin/`) |
| **Always-on rules** | `.cursor/rules/*.mdc` per project | Mode skills handle this | Mode skills handle this |
| **Mode switching** | Skills invoked via description match | `/full-ai`, `/learning`, `/manual` | `/full-ai`, `/learning`, `/manual` |
| **Install new skill** | `git pull` in `~/.codex/superpowers` | Same `git pull` | Same `git pull` |
| **Extra step** | Copy `.mdc` rule to each project | None | None |
| **Restart needed** | New session or restart | Restart Codex | New session |

## Checklist

- [ ] `skills/<skill-name>/SKILL.md` created with valid frontmatter
- [ ] (If always-active) Mode base skills updated: `full-ai`, `learning`, `manual`
- [ ] (If always-active) Mode wrapper skills updated: `full-ai-superpowers`, `learning-superpowers`, `manual-superpowers`
- [ ] (If Cursor rule) `cursor-rule.mdc` created and copied to projects
- [ ] Committed and pushed to fork
- [ ] `git pull` in `~/.codex/superpowers`
- [ ] Agent sessions restarted
