# Copilot checklist: Traceability matrix (Preflight)

REQ → design → test. Full skill: `traceability-matrix`.

## Matrix (`docs/08-traceability-matrix.md`)

Columns: Req ID | Priority | Summary | Design anchor | Test | Status

- [ ] Every Must/Should FR from `03` has a row
- [ ] Design anchor = route, file+symbol, or spec path
- [ ] Each Must FR links to ≥1 test (AT-## or automated)

## Orphan scan before "done"

- [ ] No Must FR without test
- [ ] No test without Req ID
- [ ] No Must FR without design anchor (post-implement)

## Orphan report

- [ ] List **Blocking** vs non-blocking
- [ ] Do not claim complete while Blocking ≠ empty (unless user waiver)

## Waivers

- [ ] Explicit user text if shipping with gaps

**Preflight:** https://github.com/jah-guide/preflight
