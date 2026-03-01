# Design Decisions — Claude Skill Dev & Usage

Records why the skill library is structured the way it is.
Check this before proposing changes that might contradict existing decisions.

---

## DEC-001 — Skills are plain Markdown, not code

**Decision:** Skills are `.md` files with prose instructions, not scripts or structured data formats.

**Rationale:** Claude reads natural language better than it parses DSLs. Plain Markdown
means anyone can read, write, and review a skill without tooling. Conditional logic
is expressed with **Bold** labels and indented actions — readable and sufficient for
the complexity level skills need.

**Alternatives considered:** YAML with a step schema, Python scripts that call the API,
JSON instruction sets. All rejected because they require tooling to author, review, and
debug. Markdown requires nothing.

---

## DEC-002 — Global skills live in `~/.claude/commands/`, local skills in `{project}/.claude/commands/`

**Decision:** Global skills are installed to the user-level Claude commands directory.
Local skills are installed per-project.

**Rationale:** This is how Claude Code's slash-command system works. The skill library
mirrors that directory structure so the `skills/global/` and `skills/local/` folders
map directly to install destinations. No custom discovery mechanism is needed.

---

## DEC-003 — Skills are versioned with `<!-- version: X.Y.Z -->` comments

**Decision:** Each skill file carries a version comment at the top. Versions follow
semantic rules: minor bump for step changes, patch for wording fixes.

**Rationale:** Skills are deployed to multiple projects. Without versioning, there is no
way to know if an installed skill is current or stale. The comment is invisible to users
but visible when reading the file, and is tracked in CHANGELOG.md and README.md.

---

## DEC-004 — Deployment is manual (copy-on-demand)

**Decision:** There is no auto-sync. Updating a skill in this repo does not automatically
update installed copies in other projects. The user must re-copy.

**Rationale:** Auto-deployment would require write access to all project directories or
a running sync service. Both add complexity and failure modes. Manual copy is explicit,
auditable, and requires no infrastructure. The README.md catalog tracks current versions
so it is easy to see when a deployed copy is out of date.

---

## DEC-005 — This project uses the same CI governance model as firmware-project-template-ci

**Decision:** IMPROVEMENTS.md, DECISIONS.md, CHANGELOG.md, and governance.md follow the
same structure and rules as the firmware CI project.

**Rationale:** Consistency between projects reduces cognitive switching cost. The same
improvement → approve → apply → document cycle works well for skills as it does for
firmware templates. The skill project is itself a product and benefits from the same
discipline.

---

<!-- New decisions go above this line. -->
<!-- Format:
## DEC-NNN — [Short title]
**Decision:** [What was decided]
**Rationale:** [Why this approach was chosen]
**Alternatives considered:** [What else was evaluated and why it was rejected]
-->
