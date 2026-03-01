<!-- version: 1.0.0 -->
# /simulate-user — Simulate a domain expert discovering this project for the first time

Adopt the persona of an experienced practitioner who is **new to this specific project**.
Simulate their onboarding and usage experience step by step, narrating as you go.
Flag every friction point, blocker, and weak spot. Write a structured findings report
and a prioritised action plan.

Works on any project — firmware, web app, CLI tool, library, data pipeline, etc.

---

## Step 1 — Understand the project domain

Read whatever is available, in this order:

1. `README.md` (or `README.rst`, `README.txt`) — highest priority
2. `CLAUDE.md` if present — agent briefing
3. `docs/` or `documentation/` — overview and architecture docs
4. Key config files (`platformio.ini`, `package.json`, `pyproject.toml`, `Makefile`, `docker-compose.yml`, etc.)
5. `WORKFLOW.md`, `CONTRIBUTING.md`, `SETUP.md`, `GETTING_STARTED.md` — if any exist

From what you read, determine:

- **Domain:** what field this project is in (embedded firmware, web backend, CLI tool, data pipeline, etc.)
- **Target user:** who is expected to use or work on this project
- **Entry point:** how a new user would normally start

State your persona clearly before beginning the simulation:

> "I'll simulate: a **{role}** with {N} years of {domain} experience, who has just
> found this project on GitHub. I have no prior knowledge of how this specific
> project works, its conventions, or its history."

---

## Step 2 — Narrated simulation (interactive walkthrough)

Walk through the project as the persona would, in order. Narrate every step out loud.
Do not skip ahead — experience it sequentially, as a real person would.

> "**Step 1:** I open the README. The first thing I see is..."
> "**Step 2:** I follow the setup instructions. I run `...` and..."
> "**Step 3:** Something is wrong — [what happened and why it broke]..."

**Work through these areas in order:**

### 1. First impression
- Is the project's purpose clear from the first paragraph of the README?
- Is the target audience obvious?
- Is the current state of the project clear (alpha, production-ready, template, demo)?

### 2. Prerequisites and setup
- Are prerequisites listed with specific versions?
- Are install steps complete, ordered, and free of assumed knowledge?
- What happens if a prerequisite is missing — does it fail clearly or silently?

### 3. First run / entry point
- Can the persona start using it by following only the README?
- Are there files to fill in manually? Are they clearly identified?
- What is the first observable result that confirms setup worked?

### 4. Core workflow
- What does day-to-day use look like?
- Are commands, scripts, or recurring workflows documented?
- Are there assumptions about the environment that are not stated?

### 5. Configuration and machine-specific setup
- Are there config files to fill per machine / per project?
- What happens if they are left blank, filled wrong, or missing?
- Are defaults sensible? Are required fields distinguished from optional ones?

### 6. Edge cases and failure modes
- What breaks if the persona deviates slightly from the happy path?
- What error messages appear? Are they actionable?
- What happens when things go wrong — are there recovery instructions?

### 7. Documentation completeness and consistency
- Are there references to things that don't exist?
- Are there placeholder values left unfilled?
- Do any two files contradict each other?

### 8. Continuity and handoff
- If the persona stops and comes back tomorrow, can they resume without re-reading everything?
- Is there a clear "where am I and what's next" mechanism?

**Mark every friction point inline** as you narrate using `[FINDING-N]`:
> "I try to run the script but there's no mention of Python version requirements [FINDING-3]."

---

## Step 3 — Findings report

After completing the walkthrough, write a structured report.

**Location:**
- If a `Report/` folder exists → write to `Report/user-simulation-{YYYYMMDD}.md`
- Otherwise → write to the project root as `user-simulation-{YYYYMMDD}.md`

Use this format:

```markdown
# User Simulation Report — {Project Name}

**Date:** {today's date}
**Persona:** {the role, experience level, and domain context simulated}
**Entry point:** {what document/command the persona started from}

---

## Summary

| Severity | Count |
|---|---|
| Critical | N |
| Major | N |
| Minor | N |
| **Total** | **N** |

{2–3 sentences: overall impression and the dominant theme across findings.}

---

## Findings

### [F1] — {Short descriptive title}
**Severity:** Critical / Major / Minor
**Location:** {file name and section, if applicable}
**What happened:** {what the persona encountered, in first-person terms}
**Why it matters:** {consequence if left unfixed — who gets blocked and how}

### [F2] — ...

---

## Action Plan

Severity guide:
- **Phase A — Blockers:** Critical findings. Fix before sharing the project with anyone.
- **Phase B — Major gaps:** Major findings. Fix in the next working session.
- **Phase C — Polish:** Minor findings. Fix when time permits.

### Phase A — Blockers
- **[AP-1]** {What to do and where} — fixes [F?]

### Phase B — Major gaps
- **[AP-N]** {What to do and where} — fixes [F?]

### Phase C — Polish
- **[AP-N]** {What to do and where} — fixes [F?]
```

---

## Step 4 — Closing summary

After writing the report, say:

> "**Simulation complete.**
>
> Persona: {role and domain}
> Findings: {N} total — {N Critical}, {N Major}, {N Minor}
> Biggest blocker: {one sentence describing the most severe finding}
> Report written to: `{path}`
>
> Top action items:
> — {AP-1}
> — {AP-2}
> — {AP-3}"

If any findings are Critical, say so explicitly and recommend addressing them before the next session.
