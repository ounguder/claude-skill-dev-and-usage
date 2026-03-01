# Claude Skill Dev & Usage

A dedicated project for developing, improving, and tracking Claude Code slash-command skills.

Skills are `.md` files that encode recurring workflows — Claude reads them and executes the steps
consistently, without re-explanation every session. This project is the canonical source for all
skills used across other projects.

---

## Skill Catalog

| Skill | Type | Invoke | Description | Version |
|-------|------|--------|-------------|---------|
| `/simulate-user` | Global | `/simulate-user` | Simulate a domain expert discovering a project for the first time; produces severity-ranked findings report and action plan | 1.0.0 |
| `/session-start` | Local | `/session-start` | Begin a working session: load context, start vault sync, summarise status | 1.0.0 |
| `/session-end` | Local | `/session-end` | Close a session: update HANDOFF.md, promote learnings, stop vault sync, commit | 1.0.0 |
| `/sync-vault` | Local | `/sync-vault` | Force an immediate one-shot vault sync and report results | 1.0.0 |
| `/promote` | Local | `/promote` | Promote a learning to 08 - Knowledge at any time | 1.0.0 |
| `/sync-status` | Local | `/sync-status` | Check whether vault-sync.py is running and report its PID and last sync state | 1.0.0 |

**Type:** `Global` = available on all projects on this machine · `Local` = installed per project

---

## How to Install Skills

### Global skills → available everywhere

Copy the skill file to your user-level Claude commands directory:

```powershell
copy skills\global\simulate-user.md C:\Users\ungud\.claude\commands\simulate-user.md
```

The skill is immediately available in any Claude Code session on this machine.

### Local skills → per project

Copy the skill file into the target project's `.claude/commands/` folder:

```powershell
copy skills\local\session-start.md C:\Users\ungud\Desktop\Projects\{project}\.claude\commands\session-start.md
```

Create the `.claude/commands/` directory if it does not exist yet.

---

## How to Work on This Project

Open with Claude and use one of three modes:

**Propose a new skill:**
> *"I keep having to explain X to Claude every session. Can we make a skill for it?"*

Claude designs the skill, adds a proposal to `IMPROVEMENTS.md`, and waits for approval.

**Improve an existing skill:**
> *"Apply IMP-003 — the session-end skill doesn't handle X correctly."*

Claude updates the skill file, bumps its version, and logs the change in `CHANGELOG.md`.

**Install skills into a project:**
> *"Install the session-start and session-end skills into my-project."*

Claude copies the relevant files to the correct location and confirms.

---

## Project Structure

```
claude-skill-dev-and-usage/
├── README.md              ← this file: skill catalog and quick-start
├── CLAUDE.md              ← agent briefing for this project
├── CHANGELOG.md           ← version history of the skill collection
├── IMPROVEMENTS.md        ← proposed new skills and improvements backlog
├── DECISIONS.md           ← why skills are structured the way they are
├── HOW-TO-USE-SKILLS.md   ← complete guide: writing, installing, and using skills
├── .claude/
│   └── rules/
│       └── governance.md  ← rules for how Claude works on this project
└── skills/
    ├── global/            ← deploy to: C:\Users\{you}\.claude\commands\
    │   └── simulate-user.md
    └── local/             ← deploy to: {project}\.claude\commands\
        ├── session-start.md
        ├── session-end.md
        ├── sync-vault.md
        ├── promote.md
        └── sync-status.md
```

---

## Related Repositories

| Repo | Purpose |
|------|---------|
| [firmware-project-template-ci](https://github.com/ounguder/firmware-project-template-ci) | Firmware template CI — the local skills here originate from this project |
| [claude-global-config](https://github.com/ounguder/claude-global-config) | Global Claude config and `/new-project` skill |

---

## Current Version

See [CHANGELOG.md](./CHANGELOG.md) — current version: **v1.0.0**

## Improvement Backlog

See [IMPROVEMENTS.md](./IMPROVEMENTS.md)
