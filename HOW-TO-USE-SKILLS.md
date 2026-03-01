# How to Use Claude Skills

A complete reference for understanding, writing, installing, and invoking Claude Code
slash-command skills.

---

## 1. What Are Claude Skills?

A **skill** is a `.md` file that contains step-by-step instructions Claude follows when
you invoke it with a slash command. Skills encode recurring workflows so Claude executes
them **consistently and completely**, without you having to re-explain the process every session.

**Example:** Instead of typing:
> "Read HANDOFF.md, update it with today's session status, check for knowledge to promote to
> the vault, run git status, stage all changed files, propose a commit message, ask me to
> approve, then push."

You type:
```
/session-end
```

Claude reads `session-end.md` and executes all steps in order.

---

## 2. Global vs Local Skills

| | Global | Local |
|---|---|---|
| **File location** | `C:\Users\{you}\.claude\commands\` | `{project}\.claude\commands\` |
| **Available in** | Every Claude session on this machine | Only inside that specific project |
| **Best for** | Cross-project workflows (simulation, analysis, code review) | Project-specific workflows (session management, vault sync) |
| **Examples** | `/simulate-user`, `/new-project` | `/session-start`, `/session-end`, `/sync-vault` |

---

## 3. Prerequisites

| Requirement | Needed for |
|-------------|-----------|
| [Claude Code](https://claude.ai/download) | All skills |
| Python 3.x | Local skills (runs `vault-sync.py`) |
| Obsidian + vault-sync.py | Local skills (session management, vault sync) |
| firmware-project-template-ci project setup | Local skills (full infrastructure) |

---

## 4. How to Install Skills

### Global skill

```powershell
# Copy once — available immediately in all sessions
copy skills\global\simulate-user.md C:\Users\{your-username}\.claude\commands\simulate-user.md
```

### Local skill (into an existing project)

```powershell
# Create the commands directory if it doesn't exist
mkdir {project}\.claude\commands

# Copy the skill
copy skills\local\session-start.md {project}\.claude\commands\session-start.md
```

### Verify installation

Start a Claude session in the target directory and type:
```
/help
```
Installed skills appear in the list of available slash commands.

**If the skill doesn't appear**, check:
- Global: the file must be directly in `C:\Users\{your-username}\.claude\commands\` (not a subdirectory)
- Local: the file must be in `{project-root}\.claude\commands\` (not nested further)
- The filename must match exactly: `simulate-user.md` → `/simulate-user`

---

## 5. How to Invoke a Skill

In any Claude Code session, type the skill name as a slash command:

```
/simulate-user
/session-start
/session-end
/sync-vault
/promote
/sync-status
```

Claude reads the corresponding `.md` file and begins executing the steps.

### Passing context at invocation

Some skills accept context after the command name:

```
/promote          ← skill asks what to promote
/promote ESP32 I2C clock-stretch bug    ← context provided upfront, skill proceeds faster
```

If the skill needs information it doesn't have, it will ask.

### Mid-skill interaction

Skills often pause for your input — to approve a commit message, confirm a note should be
created, or choose between options. You can also interrupt at any point and say what to
change. Claude will adapt and continue.

---

## 6. How Skills Are Structured

A skill file is a Markdown document. Claude reads it top to bottom and treats each section
as an instruction. There is no special syntax — plain English with clear steps.

### Minimal skill

```markdown
# /greet — Greet the user

Say hello to the user and ask what they want to work on today.
Print the current date and the project name from CLAUDE.md.
```

### Full skill structure (recommended for complex skills)

```markdown
# /skill-name — Short description

One sentence describing what this skill does and when to use it.

---

## Step 1 — {What happens}

{Clear instructions for this step.}

**If {condition}:**
> "{What to say to the user}"

**If not:**
- Do {X}
- Then {Y}

---

## Step 2 — {Next step}

Run:
\```
{command}
\```

Read the output and {do something with it}.

---

## Step 3 — Done

Say:
> "{Closing message}"
```

### Key conventions

| Element | Convention |
|---------|-----------|
| Steps | Numbered, each with a clear action verb header |
| User-facing messages | Quoted with `>` so you can see exactly what Claude will say |
| Commands to run | In fenced code blocks |
| Conditional branches | **Bold** condition label, indented action |
| File reads/writes | Explicit: "Read `docs/HANDOFF.md`", "Write to `Report/{filename}.md`" |
| User approval | Always ask before destructive or visible actions (git push, file delete) |

---

## 7. Writing Your Own Skill

### Before you start

Ask: *Is this workflow something I explain to Claude more than once a month?*
If yes — it's a good skill candidate.

### Step-by-step

1. **Name the skill** — kebab-case, verb-first: `session-end`, `sync-vault`, `simulate-user`
2. **Write the header** — `# /{name} — Short description`
3. **List the steps** — in the order Claude should execute them
4. **Be explicit about decisions** — what to ask the user, what to do without asking
5. **Write user-facing messages verbatim** — use `>` quotes so the output is predictable
6. **Add conditionals** for the cases that matter — missing file, empty output, failure

### What makes a good skill

- **Complete:** Every step is specified. Claude should not have to guess what comes next.
- **Deterministic:** Two runs of the same skill on the same project should produce the same result.
- **Pauseful:** The skill asks before doing anything hard to reverse (git push, file deletion).
- **Scoped:** One skill does one thing. Chain skills if you need a longer workflow.

### What to avoid

- **Vague verbs:** "Handle it", "do the right thing", "figure out". Be specific.
- **Missing failure branches:** What happens if the file doesn't exist? If git fails? Specify.
- **Too much in one skill:** If a skill has more than 6–8 steps, consider splitting it.

---

## 8. Skill Versioning

Skills in this project are versioned. Each skill file has a version comment at the top:

```markdown
<!-- version: 1.2.0 -->
# /session-end — Close a working session
```

Version bumps follow the same rules as the CI repo:

| Change | Bump |
|--------|------|
| New step added | Minor (1.X.0) |
| Existing step changed significantly | Minor (1.X.0) |
| Wording fix, typo, clarification | Patch (1.0.X) |

When a skill changes, update:
1. The version comment in the skill file
2. `CHANGELOG.md` — add an entry under the skill name
3. `README.md` — update the version in the skill catalog table
4. Re-deploy to all installed locations (copy the updated file)

---

## 9. Deploying Updated Skills

When you update a skill in `skills/global/` or `skills/local/`, you need to re-copy it
to wherever it is installed:

```powershell
# Re-deploy a global skill
copy skills\global\simulate-user.md C:\Users\{your-username}\.claude\commands\simulate-user.md

# Re-deploy a local skill to a specific project
copy skills\local\session-end.md {project}\.claude\commands\session-end.md
```

There is no auto-sync — deployment is manual. The `README.md` skill catalog tracks which
version is current so you know when a deployed copy is out of date.

---

## 10. Quick Reference

| Task | How |
|------|-----|
| Install a global skill | Copy from `skills/global/` to `~\.claude\commands\` |
| Install a local skill | Copy from `skills/local/` to `{project}\.claude\commands\` |
| Invoke a skill | Type `/skill-name` in a Claude session |
| Check available skills | Type `/help` in a Claude session |
| Propose a new skill | Tell Claude what workflow you want to encode — it adds to `IMPROVEMENTS.md` |
| Improve a skill | "Apply IMP-NNN" — Claude updates the file and bumps the version |
| See what changed | Read `CHANGELOG.md` |
| Understand a design choice | Read `DECISIONS.md` |
