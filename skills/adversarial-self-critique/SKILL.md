---
name: adversarial-self-critique
description: >-
  Stress-tests agent output with adversarial critique using a blocker/major/minor
  severity rubric, at most two revise passes, and a mandatory stress-tested note
  on ship. Use before delivering specs, plans, code summaries, PR descriptions,
  or user-facing answers when quality and risk matter; supports explicit user
  waiver to ship with known blockers.
---

# Output stress-test (adversarial critique)

## Purpose

Act as a **hostile reviewer** of your own draft before the human relies on it. Find logic gaps, missing edge cases, unstated assumptions, and overconfident claims.

This is not politeness pass — it is a structured defect hunt with a fixed revise budget.

## When to use

- Before sending a spec, plan, or requirements baseline
- Before “done”, “fixed”, or “tests pass” claims
- Before merging high-risk PRs
- When the user asks for review, sanity check, or second opinion

Skip for trivial acknowledgments or pure copy-paste of user-provided text.

## Severity rubric

| Severity | Definition | Ship default |
|----------|------------|--------------|
| **Blocker** | Wrong, unsafe, contradicts requirements, missing Must coverage, or claim without evidence | **Do not ship** |
| **Major** | Likely failure in real use, serious maintainability/security concern, ambiguous Must path | Fix or waive explicitly |
| **Minor** | Clarity, style, nice-to-have test, non-critical doc gap | May ship with note |

Classification rules:

- Untested “passes” / “works” → **Blocker**
- Scope creep without CR → **Major**
- Missing comma in internal note → **Minor**

## Process (max 2 revise passes)

```
DRAFT ──→ CRITIQUE ──→ REVISE ──→ CRITIQUE ──→ REVISE? ──→ SHIP DECISION
              │                      │
              └── pass 1             └── pass 2 (final)
```

**Pass limit:** At most **two** full revise passes after the initial draft. If blockers remain after pass 2:

- Stop revising in a loop
- Present remaining defects
- Ask for **explicit waiver** or human direction

Do not start pass 3 automatically.

### Step 1: Stabilize the artifact

Name what is being reviewed (file paths, PR, message scope).

### Step 2: Adversarial critique (structured)

Produce:

```markdown
## Stress-test — [artifact name]

### Assumptions challenged
- ...

### Findings
| ID | Severity | Finding | Suggested fix |
|----|----------|---------|---------------|
| F-01 | Blocker | ... | ... |

### Blocker count: N
```

Attack vectors (use what applies):

- Requirements drift vs `03-requirements.md`
- Edge cases: empty, max, concurrent, unauthorized
- Failure modes: timeouts, partial failure, rollback
- Evidence: are verification commands cited with output?
- Security/privacy: secrets, PII, authz
- Operability: logs, metrics, support burden

### Step 3: Revise

Fix **all Blockers** and **Major** items you can within scope. Update artifact; do not hide unresolved items.

### Step 4: Second critique

Re-run table; new findings only or confirmed fixed.

### Step 5: Ship decision

| Condition | Action |
|-----------|--------|
| Zero blockers | Ship + append stress-tested note |
| Blockers + user waiver | Ship + note lists waived blockers |
| Blockers, no waiver | Do not ship; hand human the table |

## Mandatory stress-tested note

When shipping (no blockers OR waived), append to the **user-visible summary** (PR body, final chat message, or doc footer):

```markdown
---
**Stress-tested:** Adversarial self-critique completed ([0 blockers | N waived blockers: F-01, …]). Revise passes: [0–2].
```

Keep it short; link to full finding table if in a doc.

## User waiver format

Accept waiver only when explicit, e.g.:

> Ship with known blockers: F-01, F-03

Record waiver in the stress-tested note. Do not infer waiver from silence.

## Copilot / checklist mode

In environments without multi-pass autonomy, run a **single-pass** table and ask the human to confirm fixes. Full two-pass loop is native to Cursor/Claude agents.

## Integration

| Skill | When |
|-------|------|
| `requirements-engineer` | Critique before baseline approval |
| `spec-driven-development` | Critique spec+plan before implement gate |
| `traceability-matrix` | Critique orphan report |
| `verification-before-completion` | Blocker if claims lack fresh command output |

## Anti-patterns

| Anti-pattern | Fix |
|--------------|-----|
| Endless revise loops | Hard stop at 2 passes |
| Self-grade “LGTM” with no table | Always produce findings table |
| Downgrade blockers to minor to ship | Severity rubric is strict |
| Omit stress-tested note | Always append on ship |
