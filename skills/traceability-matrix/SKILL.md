---
name: traceability-matrix
description: >-
  Builds and maintains a requirements traceability matrix linking requirement
  IDs to design artifacts and tests; blocks completion when orphan requirements,
  untested Must items, or dangling tests exist. Use when FR/NFR IDs exist, before
  claiming done on a feature, before release or audit, or when the user asks for
  RTM, coverage of requirements, or proof that tests map to reqs.
---

# Traceability Matrix

## Purpose

Prove **every requirement is designed for and verified** — and that every test maps back to intent. Orphans are delivery defects, not paperwork.

Default artifact: `docs/08-traceability-matrix.md` (or project path declared in `docs/README.md`).

## When to use

- After first FR IDs are baselined
- Before marking feature complete, PR ready, or release
- When adding/removing tests or major refactors
- Audit, portfolio evidence, or compliance reviews

## Matrix schema

Minimum columns:

| Req ID | Priority | Requirement summary | Design / build anchor | Test (AT/unit/e2e) | Status |
|--------|----------|---------------------|------------------------|--------------------|--------|

**Design / build anchor** examples (pick what fits the repo):

- Route/path: `/requests/new`
- Module: `src/lib/sla.ts`
- API: `POST /api/requests`
- UI component: `SlaBadge`

**Status** values: `planned` | `implemented` | `verified` | `waived` | `deferred`

**Waived** requires user explicit waiver text in matrix footnote.

## Workflow

### 1. Seed from requirements

Import all **Must** and **Should** FR/NFR from `03-requirements.md`. Each ID gets one primary row (split only if independently testable sub-obligations have sub-IDs).

### 2. Link design

For each row, add at least one **build anchor** once implementation exists. If design is spec-only, use `docs/specs/...` path until code lands.

### 3. Link tests

Map to:

- Acceptance tests (`09-acceptance-tests.md` AT-##), and/or
- Automated test file + case name

One Must FR may map to multiple tests; every Must FR needs **≥1** verification link before `verified`.

### 4. Orphan scan (required before done)

Run checks:

| Check | Orphan means |
|-------|----------------|
| Req → test | Must/Should FR with no test link |
| Req → design | Must FR with no design anchor (post-implement) |
| Test → req | Test ID with empty Req column |
| Priority drift | Must in matrix not Must in 03 |

Output **Orphan report**:

```markdown
## Orphan report — [date]

### Blocking
- FR-05: no test mapped

### Non-blocking
- FR-12 (Should): design anchor missing

**Done gate:** BLOCKED until Blocking empty (or user waiver).
```

### 5. Done gate

```
Do NOT claim feature complete / PR ready / shipped
while any Must-row is not Status=verified (or waived)
OR Blocking orphans exist.
```

Allowed interim language: “implemented, traceability incomplete — see orphan report.”

## Maintenance rules

- New FR → add row same session
- Deleted FR → mark `retired`, do not reuse ID
- Renamed module → update anchor, keep Req ID
- Refactor-only PR → re-run orphan scan if tests moved

## Template

Use `templates/traceability-matrix.md` in this skill folder or the copy in `analysis-docs-pack/templates/docs/08-traceability-matrix.md`.

## Example row

| Req ID | Priority | Summary | Design anchor | Test | Status |
|--------|----------|---------|---------------|------|--------|
| FR-01 | Must | Capture service request | `app/requests/new/page.tsx`, `createRequestAction` | AT-01, `tests/requests/create.test.ts` | verified |

## Integration

| Skill | Role |
|-------|------|
| `requirements-engineer` | Source of Req IDs |
| `spec-driven-development` | Plan lists expected anchors |
| `adversarial-self-critique` | Critique orphan report before ship |

## Anti-patterns

| Anti-pattern | Fix |
|--------------|-----|
| Matrix updated only at release | Update per FR completion |
| Vague anchors (“the form”) | File + symbol or route |
| Tests with no Req | Delete or link |
| Marking verified without running tests | Pair with verification evidence |
