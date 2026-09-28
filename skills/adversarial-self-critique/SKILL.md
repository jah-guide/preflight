---
name: adversarial-self-critique
description: >-
  Stress-tests agent output with adversarial critique using a blocker/major/minor
  severity rubric, ambiguity detection, phase-scoped checks, at most two revise
  passes, and a mandatory stress-tested note on ship. Use before delivering specs,
  plans, phase artifacts, code summaries, PR descriptions, or user-facing answers
  when quality and risk matter; supports explicit user waiver to ship with known
  blockers. Preflight v0.1.1.
---

# Output stress-test (adversarial critique)

## Purpose

Act as a **hostile reviewer** of your own draft before the human relies on it. Find logic gaps, missing edge cases, unstated assumptions, ambiguous success language, and overconfident claims.

This is not a politeness pass — it is a structured defect hunt with a fixed revise budget.

## When to use

- Before sending a spec, plan, or requirements baseline
- **Before closing a delivery phase** (phase-scoped AC and traceability only)
- Before “done”, “fixed”, or “tests pass” claims
- Before merging high-risk PRs
- When the user asks for review, sanity check, or second opinion

Skip for trivial acknowledgments or pure copy-paste of user-provided text.

## Severity rubric

| Severity | Definition | Ship default |
|----------|------------|--------------|
| **Blocker** | Wrong, unsafe, contradicts requirements, missing Must coverage, claim without evidence, or **ambiguous AC that cannot be verified** | **Do not ship** |
| **Major** | Likely failure in real use, serious maintainability/security concern, ambiguous Must path, scope creep without CR | Fix or waive explicitly |
| **Minor** | Clarity, style, nice-to-have test, non-critical doc gap | May ship with note |

Classification rules:

- Untested “passes” / “works” → **Blocker**
- Scope creep without CR → **Major**
- Weasel words without metrics (“fast”, “robust”, “user-friendly”) in AC or success criteria → **Major** (Blocker if Must path)
- Missing comma in internal note → **Minor**

### Ambiguity detection (mandatory pass)

Before filing findings, scan for:

| Signal | Example | Typical severity |
|--------|---------|------------------|
| **Untestable AC** | “System should be intuitive” | Major → Blocker if Must |
| **Floating quantifiers** | “Support many users”, “handle errors gracefully” | Major |
| **Undefined terms** | “Admin”, “active”, “valid” without glossary | Major |
| **Implicit scope** | Feature behavior inferred but not in spec/phase doc | Major |
| **Dual interpretation** | Two reasonable readings of the same sentence | Blocker if affects Must; else Major |

Record ambiguity findings with ID prefix `A-` (e.g. `A-01`) in the findings table.

## Phase-scoped mode

When `spec-driven-development` (or the human) defines **Phase Pn**:

1. **Scope the artifact** — only AC, todos, and REQ IDs listed for Pn.
2. **Do not** block phase sign-off on defects belonging to Pn+1 unless they leak into current deliverables.
3. **Do** block if this phase’s Must FR/NFR links are missing from the traceability matrix or untested.
4. Title the report: `Stress-test — Phase Pn — [artifact name]`.

If no phase context exists, run full-artifact mode (default).

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

Name what is being reviewed (file paths, PR, message scope, **phase ID if any**).

### Step 2: Adversarial critique (structured)

Produce:

```markdown
## Stress-test — [artifact name]

**Scope:** [full | Phase Pn — AC-Pn-01..]

### Assumptions challenged
- ...

### Ambiguity scan
- ...

### Findings
| ID | Severity | Finding | Suggested fix |
|----|----------|---------|---------------|
| F-01 | Blocker | ... | ... |
| A-01 | Major | ... | ... |

### Blocker count: N
```

Attack vectors (use what applies):

- Requirements drift vs `03-requirements.md` or **phase in/out scope**
- Edge cases: empty, max, concurrent, unauthorized
- Failure modes: timeouts, partial failure, rollback
- Evidence: are verification commands cited with output?
- Security/privacy: secrets, PII, authz
- Operability: logs, metrics, support burden
- **Traceability:** Must IDs for this phase → design/test links

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
**Stress-tested:** Adversarial self-critique completed ([0 blockers | N waived blockers: F-01, …]). Scope: [full | Phase Pn]. Revise passes: [0–2].
```

Keep it short; link to full finding table if in a doc.

## User waiver format

Accept waiver only when explicit, e.g.:

> Ship with known blockers: F-01, F-03

Record waiver in the stress-tested note. Do not infer waiver from silence.

## Self-improve hook

If the same finding class repeats across runs (e.g. skipped ambiguity scan, phase scope bleed):

- Propose a **concrete edit** to this skill or `spec-driven-development` / `lessons.md`
- Show the proposal to the human; **do not** auto-commit to the Preflight repo unless asked

## Copilot / checklist mode

In environments without multi-pass autonomy, run a **single-pass** table (include ambiguity scan) and ask the human to confirm fixes. Full two-pass loop is native to Cursor/Claude agents.

## Integration

| Skill | When |
|-------|------|
| `requirements-engineer` | Critique before baseline approval |
| `spec-driven-development` | Critique spec+plan; **each phase** before human gate |
| `traceability-matrix` | Critique orphan report |
| `verification-before-completion` | Blocker if claims lack fresh command output |

See also: [docs/phased-delivery-pipeline.md](../../docs/phased-delivery-pipeline.md)

## Anti-patterns

| Anti-pattern | Fix |
|--------------|-----|
| Endless revise loops | Hard stop at 2 passes |
| Self-grade “LGTM” with no table | Always produce findings table |
| Downgrade blockers to minor to ship | Severity rubric is strict |
| Omit stress-tested note | Always append on ship |
| Full-release critique for a single phase | Use phase-scoped mode |
