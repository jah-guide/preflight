---
name: requirements-engineer
description: >-
  Elicits and documents requirements through a full requirements-engineering
  loop: clarify intent, resolve conflicts, MoSCoW prioritization, and testable
  functional/non-functional requirements with acceptance criteria. Use when the
  problem is unclear, stakeholders disagree, scope is fuzzy, or before coding
  when no validated requirements exist. Includes a lightweight gate that blocks
  implementation until a problem statement and baseline FRs exist. Preflight v0.1.1
  adds deterministic clarifying questions (constrained choices) before baseline.
---

# Requirements Engineer

## Purpose

Produce **validated, testable requirements** before design or code. Requirements answer *what* and *why*; they deliberately avoid *how* unless constraints force it.

## When to use

- Greenfield product or feature
- “Build X” with no pain statement or success metrics
- Conflicting stakeholder asks
- Regulated, SLA, or audit-sensitive domains
- Before `spec-driven-development` when FR IDs do not exist yet

## Hard gate (inside this skill)

```
NO IMPLEMENTATION until all are true:
  1. Problem statement exists (current pain + impact)
  2. At least one primary stakeholder is named
  3. ≥1 Must-have FR with acceptance criteria
  4. Human acknowledged the requirements snapshot (approve or edit list)
```

**Allowed before gate clears:** interviews (chat), document drafts, examples, benchmarks, competitive notes, process diagrams.

**Blocked:** feature code, schema for the feature, “prototype in prod”, dependency adds for the feature.

Record **Gate cleared:** date + artifact path when the human approves.

## The RE loop

```
ELICIT → CLARIFY → ANALYZE → SPECIFY → VALIDATE → BASELINE
   ↑         │          │          │          │
   └─────────┴──────────┴──────────┴──────────┘
              (iterate until conflicts resolved)
```

### 1. Elicit

Gather inputs from whatever exists: user message, tickets, repo docs, regulations.

Output: **Elicitation notes** (`docs/requirements/elicitation-<slug>.md` or inline in chat).

Capture:

- Goals and anti-goals
- Current workflow (as-is hints)
- Systems and data touched
- Constraints (time, budget, compliance)
- Known risks

Ask **deterministic clarifying questions** when critical facts are missing:

| Style | When to use |
|-------|-------------|
| **Constrained choice** | Scope, priority, or mutually exclusive options |
| **Yes / No / Out of scope** | Binary behavior or deferral |
| **Bounded metric** | NFR targets (pick from tiers or specify) |
| **One-at-a-time** | When the next question depends on the answer |

State an **explicit default** if the human does not answer non-blocking items, and record it in the assumption log.

### 2. Clarify

Resolve ambiguity with the human:

- Define terms (glossary entries)
- Bound scope (“not in v1”)
- Identify implicit assumptions → explicit
- Reject open-ended “anything else?” until Must paths are testable

Use **Assumption log** table:

| ID | Assumption | Risk if wrong | Confirm? |
|----|------------|---------------|----------|

### 3. Analyze

**Conflict scan** — list pairs of asks that cannot both hold without tradeoffs.

| Conflict | Side A | Side B | Resolution options |
|----------|--------|--------|-------------------|

**Stakeholder map** (lightweight):

| Stakeholder | Interest | Influence | Success looks like |
|-------------|----------|-----------|-------------------|

Optional RACI lives in `02-stakeholders-raci.md` when using `analysis-docs-pack`.

### 4. Specify

Author or update **`03-requirements.md`** (or equivalent) with stable IDs.

#### ID conventions

| Type | Pattern | Example |
|------|---------|---------|
| Functional | `FR-##` | FR-01 |
| Non-functional | `NFR-##` | NFR-01 |
| Business rule | `BR-##` | BR-01 |
| Acceptance test | `AT-##` | AT-01 |

Never reuse IDs for different meaning. Deprecate with `Status: retired` and pointer to replacement.

#### Functional requirement template

```markdown
### FR-01 [Must] Short title

**Statement:** The system shall ...

**Rationale:** ...

**Acceptance criteria:**
- [ ] Given ... when ... then ...
- [ ] ...

**Dependencies:** FR-.., external systems

**Notes / open issues:** ...
```

#### Non-functional requirement template

```markdown
### NFR-01 Performance — API read latency

**Statement:** 95th percentile read latency ≤ 300ms under nominal load.

**Measure:** ...

**Acceptance criteria:**
- [ ] Load test at X RPS for Y minutes meets threshold
```

#### MoSCoW

Every FR/NFR gets exactly one: **Must | Should | Could | Won't (this release)**.

Rules:

- **Must** = launch blocker; product fails without it
- **Should** = important; workaround exists
- **Could** = desirable if time permits
- **Won't** = explicit deferral (not “maybe later” silence)

Cap **Must** items — if everything is Must, force-rank with the human.

### 5. Validate

**Quality checklist** (each FR/NFR):

- [ ] **Atomic** — one obligation per ID
- [ ] **Testable** — acceptance criteria are observable
- [ ] **Unambiguous** — no weasel words (“fast”, “user-friendly”) without metrics
- [ ] **Feasible** — known tech/org constraints respected
- [ ] **Traceable** — will link to design/tests later

Run a **read-back**: summarize requirements in plain language and ask:

> Does this match what you need? Reply **approve baseline** or list corrections.

### 6. Baseline

On approval, mark document header:

```markdown
**Baseline:** approved YYYY-MM-DD by <role/name>
**Version:** 0.1
```

Downstream skills treat baselined IDs as stable unless change control is invoked.

## Change control (after baseline)

New asks → **change request** mini-record:

| CR | Date | Request | Impact (FR/NFR) | Decision |
|----|------|---------|-----------------|----------|

Implement only after CR accepted.

## Deliverables

| Artifact | Location |
|----------|----------|
| Requirements doc | `docs/03-requirements.md` |
| Elicitation notes | `docs/requirements/elicitation-*.md` |
| Glossary | section in 03 or `docs/glossary.md` |

See `templates/requirements-doc-starter.md` in this skill folder.

## Anti-patterns

| Anti-pattern | Fix |
|--------------|-----|
| Solution masquerading as requirement | Rewrite as outcome + constraint |
| Acceptance criteria that restate the FR | Add Given/When/Then behavior |
| Missing NFRs for security/perf | Explicit NFR-## |
| Coding to “figure out requirements” | Spike only with `SPIKE` label + discard plan |

## Integration

| Skill | When |
|-------|------|
| `analysis-docs-pack` | Scaffold full 01–09 pack |
| `spec-driven-development` | After baseline FRs exist; phased Q&A → plan → gates |
| `traceability-matrix` | Once FR IDs stable |
| `adversarial-self-critique` | On requirements doc before baseline sign-off |

## Self-improve loop

If elicitation repeatedly misses the same class of gap (stakeholder, NFR, boundary):

- Propose edits to this `SKILL.md` or `skills/requirements-engineer/lessons.md`
- Show the human; do **not** auto-commit to Preflight unless asked

Downstream phased delivery: [docs/phased-delivery-pipeline.md](../../docs/phased-delivery-pipeline.md)
