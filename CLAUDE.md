# Project Manager Skills — Claude Code Skills Library

**Repo:** `github.com/nicolaas-spijker/project-manager-skills` (personal account, hosted under SignalRoads identity for trust attribution)
**Local path:** `~/project-manager-skills/`

## What this project is

An open-source Claude Code skills library for project management, modeled on Corey Haines's `marketing-skills` repo (19.6K stars). Distributed via GitHub, runs inside Claude Code (claude.ai/code or the desktop/IDE versions).

The library has two tiers:

- **Tier 1 — Prompt-only (~35 skills):** self-contained PM frameworks. Output text the user copy-pastes wherever. No API, no auth, no Rock account required. This is the audience-acquisition layer.
- **Tier 2 — Rock-connected (~15 skills):** same skills with an optional push step. Materialize tasks, notes, sprints, and chat messages directly into a user's Rock space via the bot API. This is the conversion layer.

The funnel: Tier 1 wins GitHub stars + organic discovery, Tier 2 turns that audience into Rock signups by demonstrating the platform's "BYOK AI at no surcharge" pitch in a tangible way.

## Audience

- Non-technical agency owners and PMs in Manila, Mexico City, Lagos, Jakarta, Karachi.
- Already using ChatGPT/Gemini for client work. B2/C1 English.
- Want to plan client work fast without learning to code.
- They get Claude Code installed by following our README, paste a Rock bot key once, and use `/sprint-planner` like a slash command.

## Working principles

1. **Be critical, not agreeable.** Push back on ideas honestly. If a skill doesn't earn its slot in the library, cut it.
2. **No shortcuts.** Each skill must work end-to-end before it ships. Test in Claude Code before committing.
3. **Confirm before destructive Rock API calls.** Tier 2 skills must show the user what will be created and ask for confirmation before pushing to their space. A skill that creates 30 unwanted tasks once will be uninstalled forever.
4. **Plain language.** ICP is B2/C1 English. No jargon, no MBA-speak. "Run a sprint" not "execute on velocity-aligned iteration cycles."
5. **Avoid emdashes in user-facing copy.** Use periods, commas, or colons. Internal docs (this file) can use them freely.
6. **Helpful > salesy.** Tier 1 skills must be genuinely useful to people who never sign up for Rock. Sales pressure kills the distribution flywheel.

## Skill format

Each skill is its own folder under `skills/`:

```
skills/
  sprint-planner/
    SKILL.md          # the skill itself, loaded by Claude Code
    examples/         # optional: sample inputs and outputs
    README.md         # optional: extra docs for GitHub readers
```

`SKILL.md` follows Claude Code's skill convention. Frontmatter:

```yaml
---
name: sprint-planner
description: Use when a user wants to plan a sprint of any length. Outputs goals, capacity plan, ceremonies, and a task list.
tier: 1
---
```

Body sections (use these as a consistent template):

1. **Goal** — one paragraph on what this skill does and when to use it.
2. **Inputs** — the questions the skill should ask the user before generating output. Keep to 3-5 questions max.
3. **Process** — step-by-step internal logic Claude follows.
4. **Output** — the exact structure of what gets returned (markdown, table, list, etc.).
5. **For Tier 2 only — Push step:** the API calls to make against the Rock bot API, in order. Include a confirmation prompt before the first write.

## Rock Bot API reference (for Tier 2 skills)

Tier 2 skills call the Rock bot API to create tasks, notes, and chat messages in a user's space.

- **Base URL:** `https://api.rock.so/webhook/bot`
- **Auth:** query param `?auth=<token>` or header `Authorization: Bearer <token>`
- **Method dispatch:** pass `method` as a query parameter, not a URL path segment.
  - Correct: `https://api.rock.so/webhook/bot?auth=<token>&method=getBotInfo`
  - Wrong (404): `https://api.rock.so/webhook/bot/getBotInfo?auth=<token>`
- **Docs:** https://raw.githubusercontent.com/shinyinc/rock-website-webflow/main/rock-api.html
- **Each bot is scoped to one space.** A user with multiple client spaces needs one key per space and swaps which key is loaded depending on the skill run. This is acceptable UX (mirrors how agency owners already think: "I'm working on Acme today").

### Available endpoints

- `POST sendMessage` — post a chat message in the space
- `POST createTask` — create a task with title, description, assignees, due date, list
- `POST createNote` — create a note with rich-text body
- `GET getBotInfo` — sanity-check the key works
- `GET getTaskLists` — list task lists in the space
- `GET getCustomFields` — list custom fields configured on the space
- `GET listLabels` — list labels for tagging tasks
- `GET listSpaceMembers` — list members for assignment
- `GET listSprints` — list sprints (Unlimited plan only)

### Known API gaps (do not promise these in v1)

- No `createSpace` — the user must pre-create the space, then run the skill against it.
- No `listSpaces` — skills cannot let the user pick a space at runtime; the loaded key dictates which space.
- No `setDueDate` standalone — set due dates inside `createTask` payloads.
- No file attachment endpoint — skills cannot upload files.

If a skill's value depends on these missing endpoints, queue it for v2 instead of shipping a half-version.

### How users provide their key

- Tier 2 skills read the key from an environment variable: `ROCK_BOT_API_KEY`.
- The README walks the user through:
  1. Create a Rock space (if they do not have one).
  2. Generate a bot in space settings → Integrations.
  3. Copy the bot key.
  4. Paste it as `ROCK_BOT_API_KEY` in their Claude Code project settings.
- Switching between client spaces means swapping the key. Document this clearly. The skill should call `getBotInfo` first and echo back "Connected to: <space name>" so the user is sure they hit the right space before pushing.

## The 50 skills

### Tier 1 — Prompt-only (35 skills)

**Project planning (8)**
1. `sprint-planner` — sprint of any length with goals, capacity, ceremonies, task list
2. `project-brief` — turn loose notes or a transcript into a structured brief
3. `scope-of-work` — SOW from a client conversation
4. `raid-log` — risks, assumptions, issues, dependencies tracker
5. `stakeholder-map` — power/interest grid with engagement plan per stakeholder
6. `raci-matrix` — roles per task or workstream
7. `project-charter` — high-level project framing for kickoff
8. `milestone-map` — backwards plan from a deadline

**Sprints and ceremonies (6)**
9. `sprint-kickoff` — agenda + intro doc for sprint start
10. `sprint-retro` — themes + action items from raw retro notes
11. `standup-runner` — async standup template per teammate
12. `sprint-review-prep` — demo agenda and talking points
13. `backlog-grooming` — prioritization + rough sizing
14. `sprint-velocity-tracker` — read past sprint outputs, return velocity report

**Client work (8)**
15. `client-onboarding` — week-by-week first 30 days for a new client
16. `client-kickoff-agenda` — 60-min meeting agenda
17. `client-status-report` — weekly update template
18. `discovery-questionnaire` — 20 questions for a new client engagement
19. `proposal-builder` — proposal from a brief
20. `change-request` — scope-change framing with impact analysis
21. `handoff-doc` — internal-to-client (or team-to-team) handoff
22. `client-feedback-summarizer` — distill long feedback into themes + actions

**Risk and process (5)**
23. `risk-register` — identify and score risks
24. `dependency-tracker` — surface blockers across workstreams
25. `retro-by-format` — 4Ls, Sailboat, Mad-Sad-Glad, Start-Stop-Continue
26. `post-mortem` — incident review with timeline + root cause + actions
27. `lessons-learned` — end-of-project review

**Strategy and frameworks (8)**
28. `swot-builder`
29. `vrio-analyzer`
30. `moscow-prioritizer`
31. `eisenhower-prioritizer`
32. `okrs-quarterly`
33. `kpi-dashboard-spec` — define what to measure for a project
34. `porters-five-forces`
35. `pestel-scan`

### Tier 2 — Rock-connected push skills (15)

Each Tier 2 skill should be the natural extension of a Tier 1 skill. The user runs Tier 1 to draft, then Tier 2 to push.

36. `push-sprint` — create sprint + tasks + labels in the connected space
37. `push-onboarding` — full client onboarding tasks + welcome note
38. `push-project-from-brief` — convert a brief into a task list
39. `push-retro-actions` — create tasks from retro themes
40. `push-kickoff-pack` — kickoff note + first-week tasks + intro chat message
41. `push-status-report` — post status to chat + save as note
42. `push-raid-log` — RAID log as a note in the space
43. `push-okrs-tasks` — OKRs as tasks with labels
44. `push-content-calendar` — content tasks with due dates and labels
45. `push-launch-plan` — launch checklist as a task list
46. `push-bug-triage` — bug labels + initial triage tasks
47. `push-recurring-tasks` — set up a recurring weekly/monthly task pattern
48. `push-sprint-retro` — retro note + action tasks
49. `push-stakeholder-update` — note + chat post for stakeholders
50. `push-meeting-notes` — turn meeting notes into a note + tasks for action items

## Building order (do not write all 50 at once)

The first two skills are the test of whether this whole library is worth building. Spend real care on them.

1. **Skill #1 — `sprint-planner` (Tier 1).** Prove the prompt-only architecture. End-to-end test in Claude Code. The output should be good enough that a non-Rock user finds it useful on its own.
2. **Skill #2 — `push-sprint` (Tier 2).** Same logic, but ends in API calls to a real Rock space. Test against a throwaway space first. Validate: confirmation flow, error handling on bad keys, what happens if the space already has tasks with the same names.
3. **Audit step.** What worked? What was painful? What API gaps surfaced? Update this CLAUDE.md with findings.
4. **Then scale.** Build the remaining 48 in batches of 5, testing each batch end-to-end before moving on.

## Distribution plan (when ready)

- Repo name: `project-manager-skills` on GitHub (public), hosted under `nicolaas-spijker` (personal account, audience-led naming so non-Rock visitors don't filter themselves out at the search stage).
- README must include:
  - One-paragraph pitch.
  - 30-second video of a Tier 2 skill running end-to-end (sprint appearing in Rock).
  - Install instructions for Claude Code (link to claude.ai/code, "Install Claude Code in 2 minutes").
  - How to use Tier 1 skills (no setup needed).
  - How to use Tier 2 skills (4-step screenshot guide for getting a Rock bot key).
  - Full skill list with one-line descriptions, grouped by category.
- Launch path: LinkedIn post + Indie Hackers + r/projectmanagement + relevant Slack/Discord PM communities.

## Things to NOT do

- Do not invent skills outside the 50 above without revisiting the strategy. Library scope creep kills polish.
- Do not ship a Tier 2 skill without a Tier 1 skill backing it. Every push skill needs a draft step.
- Do not push to a real Rock space during development. Use a dedicated test space.
- Do not promise functionality that depends on missing API endpoints (`createSpace`, `listSpaces`, file uploads).
- Do not name skills `rock-X` if they are Tier 1. Tier 1 skills should be platform-neutral so they read as broadly useful, not Rock-marketing.

## Reference

- Corey Haines's `marketing-skills` repo for format and tone reference: https://github.com/coreyhaines/marketing-skills (or whichever the canonical URL is — verify before linking).
- Rock product docs: https://rock.so/help
- Rock bot API docs: https://raw.githubusercontent.com/shinyinc/rock-website-webflow/main/rock-api.html
