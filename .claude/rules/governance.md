# Skill Project Governance Rules

These rules apply when working inside `claude-skill-dev-and-usage/`.

---

## Core Principle

**A skill is a product. Every change is deliberate.**

Skills are not modified casually. Each improvement is proposed, reviewed, applied, and
documented. The goal is a library of skills that gets measurably better over time.

---

## Before Changing Any Skill File — ALWAYS

1. Read `IMPROVEMENTS.md` — check if this change is already tracked
2. Read `DECISIONS.md` — check if this contradicts an existing design decision
3. State the rationale before applying
4. After applying: update the version comment in the file, update `CHANGELOG.md`,
   update the version in the `README.md` catalog table

---

## Version Bumping Rules

Version comments live at the top of each skill file: `<!-- version: X.Y.Z -->`

| Type of change | Bump |
|---------------|------|
| New step added or removed | Minor (0.X.0) |
| Existing step changed significantly | Minor (0.X.0) |
| Wording fix, typo, clarification | Patch (0.0.X) |

The overall collection version in `CHANGELOG.md` follows the same scheme,
using the highest bump of any skill changed in the release.

---

## Proposing a New Skill

When the user describes a workflow they want to encode:

1. **Evaluate:** Is this recurring (more than once a month)? Is it deterministic?
   Does it have clear steps? Could it go wrong if done inconsistently?
2. **Check type:** Global (cross-project) or local (project-specific)?
3. **Check duplicates:** Does a similar skill already exist in `skills/`?
4. **If valid:** Add to `IMPROVEMENTS.md`:
   - Unique ID: `IMP-NNN` (next in sequence)
   - Type: Global / Local
   - Target project(s): which projects would use it
   - Problem it solves
   - Proposed steps (high-level outline)
5. **Do NOT write the skill file yet** — wait for user approval

---

## Applying an Improvement

When the user approves (e.g. "apply IMP-003"):

1. Read the improvement entry carefully
2. Write or update the skill file in `skills/global/` or `skills/local/`
3. Add or update the version comment at the top of the file
4. Move the item to the "Applied" section of `IMPROVEMENTS.md` with the version reference
5. Add an entry to `CHANGELOG.md`
6. Update the version in the `README.md` skill catalog table
7. If a design decision was made: add to `DECISIONS.md`

---

## Installing Skills

When the user asks to install a skill into a project:

1. Confirm the skill name and target project path
2. Confirm whether it is global or local
3. For **global**: copy to `C:\Users\{your-username}\.claude\commands\{skill-name}.md`
4. For **local**: copy to `{project-path}\.claude\commands\{skill-name}.md`
   (create the directory if it does not exist)
5. Confirm: "Installed `/{skill-name}` to `{path}`."
6. Add a row to `INSTALL-MANIFEST.md`: skill name, target project, full path, version installed, date.

**Do not modify the skill file during installation.** Install the file as-is.
If changes are needed, apply them first as an improvement, then install.

---

## Commit Message Format

```
skill vX.Y.Z: [brief description]

Applied: IMP-NNN — [skill name / improvement title]
Files changed: [list]
```

Example:
```
skill v1.1.0: add --context flag to /simulate-user

Applied: IMP-004 — Allow context to be passed at invocation
Files changed: skills/global/simulate-user.md, CHANGELOG.md, README.md
```
