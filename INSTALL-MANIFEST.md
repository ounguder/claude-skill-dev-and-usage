# Install Manifest

Tracks which version of each skill is installed in which project.
Update this file whenever you install or re-deploy a skill.

---

## Installed Skills

| Skill | Installed In | Path | Version Installed | Date |
|-------|-------------|------|-------------------|------|
| `/simulate-user` | (global) | `C:\Users\ungud\.claude\commands\simulate-user.md` | 1.0.0 | 2026-03-01 |

---

## How to Use This File

**After installing a skill:** Add a row with the skill name, project, full path, version from the skill file's `<!-- version: X.Y.Z -->` comment, and today's date.

**After updating a skill in this repo:** Check all rows for that skill. Re-deploy to any project where the installed version is lower than the current version in the catalog.

**After removing a skill from a project:** Delete the corresponding row.

---

<!-- Add rows above as skills are installed. One row per install location per skill. -->
