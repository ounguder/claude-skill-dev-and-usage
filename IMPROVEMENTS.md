# Improvements — Claude Skill Dev & Usage

Proposed and applied improvements to the skill library.

---

## Open

No open improvements.

---

## Applied

### IMP-001 — Add infrastructure scope disclosure to README and catalog
**Type:** Documentation
**Target:** README.md
**Status:** Applied — v1.1.0
**Problem:** The README catalog presented local skills alongside the general-purpose
`/simulate-user` without any warning that local skills require the firmware/Obsidian/
vault-sync.py infrastructure. Users installing a local skill without that infrastructure
got a broken skill with no explanatory message. This was the most likely failure mode
for any new user of this project.
**Applied steps:**
- Added a callout block at the top of README.md stating that local skills require
  the firmware-project-template-ci infrastructure
- Added a "Requires" column to the skill catalog table indicating infrastructure dependencies
- Stated clearly that `/simulate-user` is the only skill that works in any project

---

### IMP-002 — Replace hardcoded username paths with placeholder
**Type:** Documentation
**Target:** README.md, HOW-TO-USE-SKILLS.md
**Status:** Applied — v1.1.0
**Problem:** Every install command hardcoded `C:\Users\ungud\`. A different user
copying the command installs to the wrong path silently — Claude doesn't show the
skill, but gives no error.
**Applied steps:**
- Replaced all `C:\Users\ungud\` occurrences in README.md with `C:\Users\{your-username}\`
- Replaced all `C:\Users\ungud\` occurrences in HOW-TO-USE-SKILLS.md with the same

---

### IMP-003 — Add Prerequisites section
**Type:** Documentation
**Target:** README.md, HOW-TO-USE-SKILLS.md
**Status:** Applied — v1.1.0
**Problem:** Neither document listed what you need before starting. Claude Code,
Python, Obsidian, and vault-sync.py were all silent dependencies discovered mid-workflow
when a skill fails at runtime.
**Applied steps:**
- Added a "Prerequisites" table to README.md listing: Claude Code, Python 3.x (local
  skills), Obsidian + vault-sync.py (local skills), firmware-project-template-ci setup
- Added a "Prerequisites" section to HOW-TO-USE-SKILLS.md before the install steps

---

### IMP-004 — Add worked example to IMPROVEMENTS.md
**Type:** Documentation
**Target:** IMPROVEMENTS.md
**Status:** Applied — v1.1.0
**Problem:** The IMPROVEMENTS.md Open section was empty and the Applied table blank.
A user returning to add their first improvement had no model to follow — the format
comment at the bottom described the fields but showed no real before/after example.
**Applied steps:**
- The full proposals IMP-001 through IMP-012 in this Applied section serve as the
  worked examples, showing the complete proposal format with all fields populated
  and "Applied" status — a new proposer can mirror this format for any Open entry

---

### IMP-005 — Add install manifest for tracking deployed copies
**Type:** Documentation
**Target:** INSTALL-MANIFEST.md (new file), README.md
**Status:** Applied — v1.1.0
**Problem:** After improving a skill, there was no way to know which projects had the
old version installed. The catalog tracked repo versions only; deployed copies could
silently run stale behavior with no indication they were outdated.
**Applied steps:**
- Created INSTALL-MANIFEST.md with a table: Skill | Installed In | Path | Version Installed
- Linked to it from README.md install section and project structure

---

### IMP-006 — Add audience and status statement to README
**Type:** Documentation
**Target:** README.md
**Status:** Applied — v1.1.0
**Problem:** README had no indication of whether this was a personal library, a
public template, or a reference project. Users who found it on GitHub couldn't tell
if the skills would work for them without reading extensively.
**Applied steps:**
- Added a callout block below the README title stating audience and which skills are
  general-purpose vs infrastructure-specific

---

### IMP-007 — Expand catalog descriptions with infrastructure requirements
**Type:** Documentation
**Target:** README.md — Skill Catalog table
**Status:** Applied — v1.1.0
**Problem:** Catalog descriptions used jargon ("vault sync", "08 - Knowledge",
"HANDOFF.md") without explanation. A new user couldn't evaluate relevance without
prior knowledge of the firmware system.
**Applied steps:**
- Added a "Requires" column to the skill catalog table
- Rewrote Description cells to be self-contained for a first-time reader

---

### IMP-008 — Add installation verification detail
**Type:** Documentation
**Target:** HOW-TO-USE-SKILLS.md — section 3
**Status:** Applied — v1.1.0
**Problem:** The guide said "Type /help — installed skills appear in the list" without
showing what to check if the skill doesn't appear. A user who installed to the wrong
path got no feedback.
**Applied steps:**
- Expanded the "Verify installation" step with: what `/help` shows and a troubleshooting
  note if the skill doesn't appear (wrong path, wrong filename, wrong directory level)

---

### IMP-009 — Link governance.md from README working modes
**Type:** Documentation
**Target:** README.md — "How to Work on This Project"
**Status:** Applied — v1.1.0
**Problem:** The three working modes section referenced the rules but didn't link to
governance.md. Users reading README.md directly had no path to the full rules and
might apply improvements or bump versions incorrectly.
**Applied steps:**
- Added a direct link to `.claude/rules/governance.md` in the "How to Work on This
  Project" section header

---

### IMP-010 — Fix versioning notation in CHANGELOG
**Type:** Documentation
**Target:** CHANGELOG.md
**Status:** Applied — v1.1.0
**Problem:** The versioning rules header used "0.X.0" notation (e.g., "Minor (0.X.0)")
but the collection was already at 1.0.0. The next minor bump is 1.1.0, making the
0.X.0 notation misleading — a user might write 0.1.0 instead of 1.1.0.
**Applied steps:**
- Changed the versioning header examples from `0.X.0` / `0.0.X` to `X.1.0` / `X.0.X`
  to match the current major version

---

### IMP-011 — Add context to Related Repositories table
**Type:** Documentation
**Target:** README.md — "Related Repositories"
**Status:** Applied — v1.1.0
**Problem:** The Related Repositories table linked to two GitHub repos without explaining
what they are, whether they are required dependencies, or what relationship they have
to this project.
**Applied steps:**
- Added a "Relationship" column to the table clarifying that these are upstream
  infrastructure repos the local skills depend on

---

### IMP-012 — Add Current State section to CLAUDE.md
**Type:** Documentation
**Target:** CLAUDE.md
**Status:** Applied — v1.1.0
**Problem:** After a week away, CLAUDE.md gave the three working modes but no orientation
— no indication of what was last changed, what improvements were in flight, or where
skills were installed. Unlike the firmware template's HANDOFF.md, this project had no
session-state mechanism.
**Applied steps:**
- Added a "## Current State" section to CLAUDE.md noting: collection version, open
  improvement count, last change summary, and pointer to INSTALL-MANIFEST.md

---

| ID | Skill / Area | Description | Version |
|----|-------------|-------------|---------|
| IMP-001 | README.md | Add infrastructure scope disclosure and catalog "Requires" column | 1.1.0 |
| IMP-002 | README.md, HOW-TO-USE-SKILLS.md | Replace hardcoded `ungud` username with `{your-username}` placeholder | 1.1.0 |
| IMP-003 | README.md, HOW-TO-USE-SKILLS.md | Add Prerequisites section | 1.1.0 |
| IMP-004 | IMPROVEMENTS.md | Add worked example proposals | 1.1.0 |
| IMP-005 | INSTALL-MANIFEST.md | Create install tracking manifest | 1.1.0 |
| IMP-006 | README.md | Add audience and status statement | 1.1.0 |
| IMP-007 | README.md | Expand catalog descriptions with requirements | 1.1.0 |
| IMP-008 | HOW-TO-USE-SKILLS.md | Add installation verification detail | 1.1.0 |
| IMP-009 | README.md | Link governance.md from working modes section | 1.1.0 |
| IMP-010 | CHANGELOG.md | Fix versioning notation | 1.1.0 |
| IMP-011 | README.md | Add context to Related Repositories | 1.1.0 |
| IMP-012 | CLAUDE.md | Add Current State section | 1.1.0 |

---

<!-- New proposals go in the Open section above. -->
<!-- Format:
### IMP-NNN — [Title]
**Type:** Global / Local / Documentation
**Target:** [project(s) or files affected]
**Status:** Proposed
**Problem:** [what gap or pain this solves]
**Proposed steps:**
- step 1
- step 2
-->
