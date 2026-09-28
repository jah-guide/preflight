# Copilot checklist: Requirements engineer (Preflight)

Use before writing feature code. Full skill: `requirements-engineer` in jah-guide/preflight.

## Gate — do not implement until ALL true

- [ ] Problem statement: current pain + impact (not only a solution idea)
- [ ] Primary stakeholder named
- [ ] ≥1 **Must** FR with Given/When/Then acceptance criteria
- [ ] Human said **approve baseline** or listed edits

## Elicit & clarify

- [ ] Scope in / out written
- [ ] Assumption log started (assumption, risk if wrong)
- [ ] Conflicts table if stakeholders disagree

## Specify

- [ ] IDs: FR-##, NFR-##; MoSCoW on each
- [ ] NFRs for security/perf when relevant
- [ ] Document at `docs/03-requirements.md`

## Validate

- [ ] Each FR atomic, testable, unambiguous
- [ ] Read-back summary to human

## After baseline

- [ ] Change requests for new scope
- [ ] Hand off to spec-plan gate before code

**Preflight:** https://github.com/jah-guide/preflight
