# Copilot checklist: Spec-driven development (Preflight)

No feature implementation until plan approved. Full skill: `spec-driven-development`.

## Before specify

- [ ] Requirements gate passed (or explicit waiver)
- [ ] Assumptions listed for human correction

## Spec (`docs/specs/<slug>.md`)

- [ ] Objective, scope, success criteria (testable)
- [ ] Commands: build, test, lint, dev
- [ ] Boundaries: always / ask first / never

## Plan (`docs/plans/<slug>-plan.md`)

- [ ] Approach + one rejected alternative
- [ ] File-level change list
- [ ] Test plan tied to FR IDs
- [ ] Top risks

## Approval

- [ ] Stop and ask: **Approve spec+plan to implement**
- [ ] Do not create feature source files until approval

## After implement

- [ ] Update traceability matrix
- [ ] Run verification before "done"

**Preflight:** https://github.com/jah-guide/preflight
