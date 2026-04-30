# Project Manager Skills

Open-source Claude Code skills library for project managers, agency owners, and small teams.

50 skills across two tiers:

- **Tier 1 (35 skills) — Prompt-only.** Self-contained PM frameworks. No setup, no account needed. Sprint planning, retros, RAID logs, stakeholder maps, OKRs, and more.
- **Tier 2 (15 skills) — Push to Rock.** Same skills, but they materialize tasks, notes, and chat messages directly into your [Rock](https://rock.so) workspace.

## Status

In development. Not yet ready for install.

## Install (when ready)

In your terminal, run:

```bash
claude plugin marketplace add nicolaas-spijker/project-manager-skills
claude plugin install project-manager-skills@project-manager-skills
```

Verify with `claude plugin list`. The plugin is installed at user scope, so it works across all your Claude Code sessions (CLI, desktop app, VS Code extension). Skills appear as slash commands, e.g. `/sprint-planner`, after restarting your Claude Code session.

### Manual install (fallback)

```bash
git clone https://github.com/nicolaas-spijker/project-manager-skills.git ~/.claude/skills/project-manager-skills
```

Restart Claude Code.

### Where this works

- Claude Code CLI, desktop app, IDE extensions (VS Code, Cursor, etc.): yes.
- claude.ai/code (web): not currently supported.
- Claude.ai chat / Claude desktop app: this repo ships Claude Code skills, not Claude.ai Skills (`.skill` packages). A `.skill`-format release may come later.

## Tier 2 setup

Tier 2 skills push to a Rock workspace. To use them:

1. Create a [Rock](https://rock.so) space (free).
2. In space settings, create a bot and copy its API key.
3. Add the key to your Claude Code project as `ROCK_BOT_API_KEY`.
4. Run any `push-*` skill.

Each bot is scoped to one space. To work across multiple client spaces, swap the key when switching spaces.

## License

MIT.
