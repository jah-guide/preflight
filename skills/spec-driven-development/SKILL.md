---
name: spec-driven-development
description: >-
  Runs a gated Q&A → specify → phased plan → per-phase implement pipeline with
  phase todos, stress-tests, and human approval between phases; blocks
  implementation until the human approves the plan. Use when starting features or
  multi-file changes, when requirements are vague, when the user asks for
  spec-first or design-before-code delivery, or before any work that would take
  more than ~30 minutes without an approved plan. Preflight v0.1.1.
---

# Spec-Driven Development

## Purpose

Turn intent into an **approved phased plan** before touching production code. The spec and plan are the contract between the agent and the human; implementation without that contract is guessing.

**Progress over perfection:** deliver in phases; each phase ends with stress-test + human gate before the next.

Pair with `requirements-engineer` when the problem itself is unclear, and with `traceability-matrix` once requirements IDs exist.

Canonical workflow doc: [docs/phased-delivery-pipeline.md](../../docs/phased-delivery-pipeline.md)

## When to use

| Use | Skip |
|-----|------|
| New feature, module, or service | One-line typo or comment fix |
| Multi-file or architectural change | Change is fully specified in the issue |
| Ambiguous or conflicting asks | Trivial config with obvious safe default |
| User says “spec first”, “plan before code” | Emergency hotfix with explicit user override |

## Hard gates

```
NO IMPLEMENTATION (code, scaffold, migrations, dependency adds)
until the human explicitly approves the PLAN artifact (including phases).
```

```
NO START on Phase P(n+1) until the human explicitly approves Phase Pn completion.
```

**Allowed before plan approval:** read repo, ask questions, draft specs/plans, spike notes labeled `SPIKE — discard`, static analysis, run existing tests.

**Not allowed before plan approval:** new source files for the feature, schema changes, new packages, CI edits for the feature, “I'll just stub it” commits.

If the user says “just do it”, treat that as **plan waiver** — record what was skipped and proceed.

## Pipeline (v0.1.1)

```
Q&A GATE ──→ REQUIREMENTS CHECK ──→ SPECIFY ──→ PHASED PLAN ──→ [PLAN APPROVE]
                                                                    │
                    ┌───────────────────────────────────────────────┘
                    ▼
              Phase Pn: TODO + IMPLEMENT ──→ STRESS-TEST ──→ [PHASE APPROVE] ──→ P(n+1) …
                    │                              │
                    └──────── self-improve ────────┘ (propose SKILL edits on repeat failures)
```

### Step 0: Q&A gate (deterministic clarifying questions)

Before drafting the spec, ask **constrained** questions — not vague “what do you want?”

Prefer:

- Multiple choice with explicit default if silent
- Yes / No / Out of scope
- Bounded options for NFRs (latency tiers, supported roles)

Record answers in the spec **Assumptions** section (corrected by human replies).

Batch independent questions; go one-at-a-time when the next question depends on the answer.

If blocking unknowns remain, list them and **pause** — do not invent a phased plan on sand.

### Step 0b: Requirements check

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

### Step 2: Phased plan

Produce a **Plan** artifact. Default path: `docs/plans/<feature-slug>-plan.md`.

Plan content:

- **Approach** — chosen design in plain language (1–2 paragraphs)
- **Alternatives considered** — at least one rejected option and why
- **Phases** — P1, P2, … each with outcome, in/out scope, AC, verification (see template)
- **File-level change list** — by phase where possible
- **Data / API / UI deltas** — schemas, endpoints, screens
- **Test plan** — which tests prove which requirements **per phase**
- **Rollout / rollback** — flags, migrations, feature toggles if relevant
- **Risks** — top 3 and mitigations

Phase artifact template: [`templates/phase-gate.md`](templates/phase-gate.md)

Keep plans proportional: a small fix might be one phase and ten lines; a subsystem might be multiple phases over two pages.

### Step 3: Plan approval gate

Stop and ask the human to review **Spec + Phased Plan**. Use explicit wording:

> Spec and phased plan are ready at `[paths]`. Approve to implement **Phase P1**, or list changes.

Do not interpret silence or “looks good” on partial sections as full approval unless the user clearly approves the **plan**.

### Step 4: Per-phase implementation

For the **current phase only**:

1. Copy or fill `templates/phase-gate.md` → `docs/plans/<slug>/P<n>.md` (or equivalent).
2. Materialize a **markdown todo checklist** tied to that phase’s AC only.
3. Implement in the order the plan states for this phase.
4. Update `traceability-matrix` when REQ IDs exist.
5. Do not expand scope; new scope → new spec/plan cycle or CR.

### Step 5: Phase stress-test

Before asking for phase approval, run `adversarial-self-critique` in **phase-scoped mode** against the phase artifact and deliverables.

Fix blockers/majors within the two-pass budget; attach stress-test summary to the phase file.

### Step 6: Phase approval gate

Stop and ask:

> Phase **Pn** complete per `[paths]`. Stress-test: [summary]. **Approve to start P(n+1)**, or list corrections.

Record approval in the phase file (`**Phase Pn approved:** date`).

**No silent phase drift** — do not begin P(n+1) without explicit approval.

Repeat steps 4–6 until all phases complete.

### Step 7: Verify (release or final phase)

Before claiming the initiative done:

- Run verification commands from the spec
- Map results to success criteria
- Run full-scope `adversarial-self-critique` on the delivery summary when the change is user-visible or high risk

## Self-improve loop

When mistakes or ambiguous output recur:

1. Name the failure mode.
2. Propose concrete edits to the relevant `SKILL.md` or `skills/<id>/lessons.md`.
3. Show the human the proposal.
4. **Do not** commit to the Preflight skill repo unless the user asks.

Document the lesson in the phase file **Self-improve notes** section when helpful.

## Artifacts checklist

| Artifact | Typical path | Approved? |
|----------|--------------|-----------|
| Spec | `docs/specs/<slug>.md` | Reviewed |
| Phased plan | `docs/plans/<slug>-plan.md` | **Required** |
| Phase gate | `docs/plans/<slug>/P<n>.md` | Per phase |
| Capability map | `docs/specs/<initiative>-capabilities.md` | If multi-module |

## Anti-patterns

| Pattern | Why it fails |
|---------|----------------|
| “I'll code while we discuss” | Locks in wrong assumptions |
| Monolithic plan with no phases | Hard to gate; ambiguous “done” |
| Skipping Q&A gate | Plan encodes wrong intent |
| Starting P2 without P1 approval | Silent scope/time drift |
| Spec without testable success criteria | No objective done signal |
| Plan that's only a task dump | No design accountability |

## Example plan approval request (agent → human)

```markdown
## Ready for plan approval

**Spec:** docs/specs/sla-dashboard-widget.md  
**Plan:** docs/plans/sla-dashboard-widget-plan.md (P1: read-only cards · P2: export)

**Summary:** P1 adds SLA summary cards on ops home; P2 adds CSV export. No new APIs in P1.

**Approve** to implement Phase P1, or reply with edits.
```

## Integration

| Skill | Relationship |
|-------|----------------|
| `requirements-engineer` | Upstream when problem/FRs missing; deterministic Q&A patterns |
| `analysis-docs-pack` | Optional parallel docs scaffolding |
| `traceability-matrix` | During/after implement, per phase |
| `adversarial-self-critique` | Before each phase gate + final ship |
