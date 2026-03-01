# Claude Skill Dev & Usage — Agent Briefing

## What This Project Is

This is a **skill development and tracking project**, not a firmware or application project.
It is the canonical source for Claude Code slash-command skills used across other projects.

Do not write application code here. Do not import styles from other projects.
Work is limited to: designing skills, improving skills, writing documentation, and maintaining the catalog.

## How to Work Here

See @.claude/rules/governance.md for the full rules.

Three modes:

**Propose a new skill:**
The user describes a recurring workflow they want to encode. Evaluate whether it is a good
skill candidate (recurring, clear steps, deterministic). Add to `IMPROVEMENTS.md`.
Do not write the skill file until the user approves.

**Apply an improvement:**
The user says "apply IMP-NNN". Read the improvement entry, write or update the skill file,
bump its version comment, update `CHANGELOG.md`, update the catalog in `README.md`.

**Install skills into a project:**
The user names a project and a skill. Copy the skill file to the correct location and confirm.
If it is a global skill: `~\.claude\commands\`.
If it is a local skill: `{project}\.claude\commands\`.

## IMPORTANT Rules
See @.claude/rules/governance.md

## Skill Catalog
See @README.md

## Version History
See @CHANGELOG.md
