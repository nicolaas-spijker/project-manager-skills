# Project Manager Skills

**The easiest way to use AI for project management. Built for agency owners and PMs who already use ChatGPT or Claude in the browser.**

Forty free, ready-to-use slash commands for sprint planning, retros, client briefs, OKRs, RAID logs, stakeholder maps, and more. They run inside Claude Code (Anthropic's free desktop app for chatting with Claude on your computer). Each skill produces a plan you can paste into any project tool. If you use [Rock](https://rock.so), one extra step pushes the plan directly into your workspace as tasks, notes, and a kickoff message.

If you've used ChatGPT to draft a sprint plan or organize a client kickoff, this is the next step. Same kind of conversation, but the workflows are now one-word commands you can rerun whenever you need them.

## Status

In development. Not yet ready for install.

## What you need before installing

1. **Claude Code installed.** Free. Download it from [claude.ai/download](https://claude.ai/download). Takes about 2 minutes. You don't need to know how to code to use it — it works like a chat app.
2. **A terminal.** On Mac, that's the Terminal app (already installed). On Windows, PowerShell. You'll paste two lines into it. That's it.

## Install (when ready)

Open your terminal and paste these two lines:

```bash
claude plugin marketplace add nicolaas-spijker/project-manager-skills
claude plugin install project-manager-skills@project-manager-skills
```

Restart Claude Code. Now in any chat, type `/sprint-planner` (or any other skill name) and it runs. That's the whole install.

### What if I don't want to use the marketplace?

Drop into your terminal and run:

```bash
git clone https://github.com/nicolaas-spijker/project-manager-skills.git ~/.claude/skills/project-manager-skills
```

Restart Claude Code. Same outcome.

## Try it

Open Claude Code, type `/sprint-planner`, and answer four short questions: sprint goal, work scope and timeline, team and availability, effort estimates per task. You get a complete sprint plan you can paste into Notion, Jira, Linear, Trello, Asana, or Rock.

If you use Rock, the plan ends with a one-line offer: say "push to Rock" and the sprint, tasks (with checklists), assignees, and a kickoff chat message land directly in your space. Setup for that is a one-time, four-step thing — full instructions below.

## Connect to Rock (optional)

Skills work fine without Rock. But if you want them to push tasks and plans directly into a workspace, here's how to wire it up. One time, four steps:

1. Sign up for a free [Rock](https://rock.so) account.
2. Create a space for the project or client you're planning.
3. In the space settings, go to Integrations → create a bot. Copy the bot's API key.
4. In your Claude Code project, set the key as an environment variable: `ROCK_BOT_API_KEY=<your key>`.

That's it. From now on, any skill that offers a Rock push will work. Switching between client spaces is as simple as swapping the key.

## Skill list

Coming as skills land. The full list of ~40 unified skills lives in [CLAUDE.md](CLAUDE.md).

The first one is `/sprint-planner`. Try it and tell me if it's useful.

## Where this works

- Claude Code desktop app, CLI, and IDE extensions (VS Code, Cursor): yes.
- claude.ai/code (the web version): not yet supported by Anthropic for plugins.
- Regular ChatGPT or Claude.ai chat: not supported (this is built for Claude Code, not the chat apps).

## License

MIT. Use it however you want.
