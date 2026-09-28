---
name: spec-driven-development
description: >-
  Runs a gated specify → plan → implement pipeline and blocks implementation
  until the human approves the plan. Use when starting features or multi-file
  changes, when requirements are vague, when the user asks for spec-first or
  design-before-code delivery, or before any work that would take more than
  ~30 minutes without an approved plan.
---

# Spec-Driven Development

## Purpose

Turn intent into an **approved plan** before touching production code. The spec and plan are the contract between the agent and the human; implementation without that contract is guessing.

Pair with `requirements-engineer` when the problem itself is unclear, and with `traceability-matrix` once requirements IDs exist.

## When to use

| Use | Skip |
|-----|------|
| New feature, module, or service | One-line typo or comment fix |
| Multi-file or architectural change | Change is fully specified in the issue |
| Ambiguous or conflicting asks | Trivial config with obvious safe default |
| User says “spec first”, “plan before code” | Emergency hotfix with explicit user override |

## Hard gate

```
NO IMPLEMENTATION (code, scaffold, migrations, dependency adds)
until the human explicitly approves the PLAN artifact.
```

**Allowed before approval:** read repo, ask questions, draft specs/plans, spike notes labeled `SPIKE — discard`, static analysis, run existing tests.

**Not allowed before approval:** new source files for the feature, schema changes, new packages, CI edits for the feature, “I'll just stub it” commits.

If the user says “just do it”, treat that as **plan waiver** — record what was skipped and proceed.

## Pipeline

```
REQUIREMENTS CHECK ──→ SPECIFY ──→ PLAN ──→ [APPROVE] ──→ IMPLEMENT ──→ VERIFY
        │                  │          │           │
        │                  └──────────┴───────────┘
        │                     human review
        └── invoke requirements-engineer if no problem statement / FRs
```

### Step 0: Requirements check

Before specifying, confirm:

- [ ] Named **problem** (pain or opportunity), not only a solution sketch
- [ ] Primary **users/stakeholders**
- [ ] At least one **testable success condition**

If any box is empty, run `requirements-engineer` (or finish it) before Specify.

### Step 1: Specify

Produce a **Spec** artifact. Default path: `docs/specs/<feature-slug>.md` (or project convention).

**Surface assumptions first** — list what you are inferring and ask for correction:

```markdown
## Assumptions (confirm or correct)
1. ...
2. ...
```

**Spec sections (adapt to size):**

1. **Objective** — outcome, users, non-goals
2. **Scope** — in / out for this iteration
3. **Requirements summary** — pointer to FR/NFR IDs if they live in `03-requirements.md`
4. **Constraints** — tech, compliance, performance, timeline
5. **Commands** — build, test, lint, dev (full commands)
6. **Structure** — where code, tests, and docs live
7. **Testing strategy** — levels, frameworks, coverage expectations
8. **Boundaries** — always / ask first / never
9. **Success criteria** — testable checklist
10. **Open questions** — unresolved items blocking plan

**Scope check (multi-capability requests only):** if one ask bundles several independently shippable capabilities, draft a short **capability map** (module id, responsibility, dependencies, build order) and get human approval before per-module specs.

### Step 2: Plan

Produce a **Plan** artifact. Default path: `docs/plans/<feature-slug>-plan.md`.

Plan content:

- **Approach** — chosen design in plain language (1–2 paragraphs)
- **Alternatives considered** — at least one rejected option and why
- **File-level change list** — create/modify/delete with purpose
- **Data / API / UI deltas** — schemas, endpoints, screens
- **Test plan** — which tests prove which requirements
- **Rollout / rollback** — flags, migrations, feature toggles if relevant
- **Risks** — top 3 and mitigations

Keep plans proportional: a small fix might be ten lines; a subsystem might be two pages.

### Step 3: Approval gate

Stop and ask the human to review **Spec + Plan**. Use explicit wording:

> Spec and plan are ready at `[paths]`. Approve to implement, or list changes.

Do not interpret silence or “looks good” on partial sections as full approval unless the user clearly approves the **plan**.

### Step 4: Implement

After approval:

- Implement in the order the plan states
- Update `traceability-matrix` when REQ IDs exist
- Do not expand scope; new scope → new spec/plan cycle

### Step 5: Verify

Before claiming done:

- Run verification commands from the spec
- Map results to success criteria
- Run `adversarial-self-critique` on the delivery summary when the change is user-visible or high risk

## Artifacts checklist

| Artifact | Typical path | Approved? |
|----------|--------------|-----------|
| Spec | `docs/specs/<slug>.md` | Reviewed |
| Plan | `docs/plans/<slug>-plan.md` | **Required** |
| Capability map | `docs/specs/<initiative>-capabilities.md` | If multi-module |

## Anti-patterns

| Pattern | Why it fails |
|---------|----------------|
| “I'll code while we discuss” | Locks in wrong assumptions |
| Spec without testable success criteria | No objective done signal |
| Plan that's only a task dump | No design accountability |
| Skipping plan for “speed” | Rework dominates savings |

## Example approval request (agent → human)

```markdown
## Ready for plan approval

**Spec:** docs/specs/sla-dashboard-widget.md  
**Plan:** docs/plans/sla-dashboard-widget-plan.md  

**Summary:** Add read-only SLA summary cards to the ops home page; no new APIs; reuse `getOpenRequestCounts`.

**Approve** to implement, or reply with edits.
```

## Integration

| Skill | Relationship |
|-------|----------------|
| `requirements-engineer` | Upstream when problem/FRs missing |
| `analysis-docs-pack` | Optional parallel docs scaffolding |
| `traceability-matrix` | During/after implement |
| `adversarial-self-critique` | Before ship on material deliverables |
