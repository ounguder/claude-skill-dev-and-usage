# Claude Skill Dev & Usage

A dedicated project for developing, improving, and tracking Claude Code slash-command skills.

> **Personal skill library.** This is a personal workflow tool, not a general-purpose framework.
> `/simulate-user` works in any project. The local skills (`/session-start`, `/session-end`, etc.)
> require the [firmware-project-template-ci](https://github.com/ounguder/firmware-project-template-ci)
> infrastructure (vault-sync.py + Obsidian vault). If you don't have that setup, only `/simulate-user`
> will work for you out of the box.

Skills are `.md` files that encode recurring workflows — Claude reads them and executes the steps
consistently, without re-explanation every session. This project is the canonical source for all
skills used across other projects.

---

## Prerequisites

| Requirement | Needed for |
|-------------|-----------|
| [Claude Code](https://claude.ai/download) | All skills |
| Python 3.x | Local skills (runs `vault-sync.py`) |
| Obsidian + vault-sync.py | Local skills (session management, vault sync) |
| firmware-project-template-ci project setup | Local skills (full infrastructure) |

See [firmware-project-template-ci](https://github.com/ounguder/firmware-project-template-ci) for
infrastructure setup instructions.

---

## Skill Catalog

| Skill | Type | Invoke | Description | Requires | Version |
|-------|------|--------|-------------|----------|---------|
| `/simulate-user` | Global | `/simulate-user` | Simulate a domain expert discovering a project for the first time; produces severity-ranked findings report and action plan | Claude Code only | 1.0.0 |
| `/session-start` | Local | `/session-start` | Begin a working session: load context from HANDOFF.md, start vault sync, summarise current project status | vault-sync.py + Obsidian | 1.0.0 |
| `/session-end` | Local | `/session-end` | Close a session: update HANDOFF.md, promote learnings to the Obsidian knowledge vault, stop vault sync, commit | vault-sync.py + Obsidian | 1.0.0 |
| `/sync-vault` | Local | `/sync-vault` | Force an immediate one-shot vault sync and report results | vault-sync.py | 1.0.0 |
| `/promote` | Local | `/promote` | Promote a learning from session notes to the long-term Obsidian knowledge base | vault-sync.py + Obsidian | 1.0.0 |
| `/sync-status` | Local | `/sync-status` | Check whether vault-sync.py is running and report its PID and last sync state | vault-sync.py | 1.0.0 |

**Type:** `Global` = available on all projects on this machine · `Local` = installed per project

---

## How to Install Skills

### Global skills → available everywhere

```powershell
copy skills\global\simulate-user.md C:\Users\{your-username}\.claude\commands\simulate-user.md
```

### Local skills → per project

```powershell
# Create the commands directory if it doesn't exist
mkdir {project}\.claude\commands

# Copy the skill
copy skills\local\session-start.md {project}\.claude\commands\session-start.md
```

### Verify installation

Start a Claude session in the target directory and type `/help`. Installed skills appear in the
list of available slash commands.

**If the skill doesn't appear**, check:
- Global: the file must be directly in `C:\Users\{your-username}\.claude\commands\` (not a subdirectory)
- Local: the file must be in `{project-root}\.claude\commands\` (not nested further)
- The filename must match exactly: `simulate-user.md` → `/simulate-user`

### Tracking installed copies

Record installed skills and their versions in [INSTALL-MANIFEST.md](./INSTALL-MANIFEST.md).
When you update a skill, check the manifest to know which projects need re-deployment.

---

## How to Work on This Project

Open with Claude and use one of three modes (full rules: [governance.md](.claude/rules/governance.md)):

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
├── INSTALL-MANIFEST.md    ← tracks which version of each skill is deployed where
├── .claude/
│   └── rules/
│       └── governance.md  ← rules for how Claude works on this project
└── skills/
    ├── global/            ← deploy to: C:\Users\{your-username}\.claude\commands\
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

| Repo | Purpose | Relationship |
|------|---------|--------------|
| [firmware-project-template-ci](https://github.com/ounguder/firmware-project-template-ci) | Firmware CI template with session management | **Upstream infrastructure** — the local skills were extracted from this project and require its vault-sync.py + Obsidian setup to function |
| [claude-global-config](https://github.com/ounguder/claude-global-config) | Global Claude config and `/new-project` skill | **Companion repo** — user-level Claude settings and additional global skills |

---

## Current Version

See [CHANGELOG.md](./CHANGELOG.md) — current version: **v1.1.0**

## Improvement Backlog

See [IMPROVEMENTS.md](./IMPROVEMENTS.md)
