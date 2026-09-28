# Copilot checklist: Output stress-test (Preflight v0.1.1)

Adversarial self-critique — single-pass in Copilot; 2-pass in Cursor/Claude. Full skill: `adversarial-self-critique`.

## Before ship (spec, phase, PR summary, "done")

Produce a findings table:

| ID | Severity | Finding | Fix |
|----|----------|---------|-----|

Severity: **Blocker** (wrong/unsafe/no evidence/ambiguous Must AC) | **Major** | **Minor**

## Ambiguity scan

- [ ] Untestable or weasel-word AC flagged (A- IDs)
- [ ] Undefined terms that affect Must paths

## Phase-scoped (if using phased delivery)

- [ ] Title scope: Phase Pn + AC IDs only
- [ ] Must traceability for this phase covered

## Attack vectors

- [ ] vs requirements / phase in-out scope / scope creep
- [ ] Edge: empty, max, auth, concurrent
- [ ] Claims vs fresh command output
- [ ] Security / PII / secrets

## Revise budget

- [ ] Fix all Blockers you can
- [ ] Max **2** full revise passes in agent environments; in Copilot ask human to re-run once

## Ship

- [ ] Zero blockers OR explicit user waiver listed
- [ ] Append stress-tested note:

`Stress-tested: adversarial critique ([0 blockers | waived F-..]). Scope: [full | Phase Pn]. Passes: N.`

**Preflight:** https://github.com/jah-guide/preflight
