# Changelog — Claude Skill Dev & Usage

All skill changes are logged here.

Versioning:
- **Minor (0.X.0):** step added, removed, or significantly changed
- **Patch (0.0.X):** wording fix, typo, clarification

Each skill file also carries its own `<!-- version: X.Y.Z -->` comment.

---

## [1.0.0] — 2026-03-01

**Initial release — skill library established from firmware-project-template-ci v3.0.0
and claude-global-config.**

### Skills Added

| Skill | Type | Version | Source |
|-------|------|---------|--------|
| `/simulate-user` | Global | 1.0.0 | Designed in this session |
| `/session-start` | Local | 1.0.0 | firmware-project-template-ci v3.0.0 |
| `/session-end` | Local | 1.0.0 | firmware-project-template-ci v3.0.0 |
| `/sync-vault` | Local | 1.0.0 | firmware-project-template-ci v3.0.0 |
| `/promote` | Local | 1.0.0 | firmware-project-template-ci v3.0.0 |
| `/sync-status` | Local | 1.0.0 | firmware-project-template-ci v3.0.0 |

### Files Established

- `README.md` — skill catalog, install instructions, working modes
- `CLAUDE.md` — agent briefing
- `CHANGELOG.md` — this file
- `IMPROVEMENTS.md` — improvement backlog
- `DECISIONS.md` — design decisions
- `HOW-TO-USE-SKILLS.md` — complete guide: what skills are, how to write, install, and invoke them
- `.claude/rules/governance.md` — rules for working on this project
- `skills/global/simulate-user.md`
- `skills/local/session-start.md`
- `skills/local/session-end.md`
- `skills/local/sync-vault.md`
- `skills/local/promote.md`
- `skills/local/sync-status.md`

---

<!-- New entries go above this line, newest first -->
