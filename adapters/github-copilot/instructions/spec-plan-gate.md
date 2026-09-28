# Copilot checklist: Spec-driven development (Preflight v0.1.1)

No feature implementation until plan approved. Full skill: `spec-driven-development`. Phased loop is Cursor/Claude-native.

## Q&A gate (before spec)

- [ ] Ask constrained questions (choices / yes-no / bounded metrics)
- [ ] Record answers in spec assumptions

## Before specify

- [ ] Requirements gate passed (or explicit waiver)
- [ ] Assumptions listed for human correction

## Spec (`docs/specs/<slug>.md`)

- [ ] Objective, scope, success criteria (testable)
- [ ] Commands: build, test, lint, dev
- [ ] Boundaries: always / ask first / never

## Phased plan (`docs/plans/<slug>-plan.md`)

- [ ] Phases P1, P2, … each with outcome + AC + verification
- [ ] Approach + one rejected alternative
- [ ] File-level change list (by phase if possible)
- [ ] Test plan tied to FR IDs
- [ ] Top risks

## Plan approval

- [ ] Stop and ask: **Approve spec+phased plan to implement Phase P1**
- [ ] Do not create feature source files until approval

## Per phase

- [ ] Phase todo checklist scoped to phase AC only
- [ ] Stress-test (findings table) before phase sign-off
- [ ] Stop and ask: **Approve Pn to start P(n+1)** — no silent phase drift

## After final phase

- [ ] Update traceability matrix
- [ ] Run verification before "done"

**Preflight:** https://github.com/jah-guide/preflight
