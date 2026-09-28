# Preflight skill map

## Pipeline view (v0.1.1)

```mermaid
flowchart LR
  RE[requirements-engineer]
  ADP[analysis-docs-pack]
  SDD[spec-driven-development]
  Pn[Phase Pn implement]
  ST[adversarial-self-critique]
  G[Human gate]
  TM[traceability-matrix]

  RE --> ADP
  RE --> SDD
  ADP --> SDD
  SDD --> Pn
  Pn --> ST
  ST --> G
  G --> Pn
  Pn --> TM
  TM --> ST
  RE -. baseline review .-> ST
  SDD -. plan review .-> ST
```

## Skill reference

| ID | Load when… | Primary output | Blocks |
|----|------------|----------------|--------|
| `requirements-engineer` | Problem vague; no FR IDs; stakeholder conflict | `03-requirements.md`, baseline | Implementation without problem + Must FR |
| `analysis-docs-pack` | Need full analyst `docs/01–09` | Scaffolded docs tree | Nothing (scaffolding only) |
| `spec-driven-development` | Multi-file feature; spec-first ask | Spec + **phased** plan + phase gate files | Code until **plan approved**; P(n+1) until **Pn approved** |
| `traceability-matrix` | FR IDs exist; pre-release | `08-traceability-matrix.md`, orphan report | “Done” with Must orphans |
| `adversarial-self-critique` | Before phase gate or ship; high-risk answer | Findings table + stress-tested note | Ship with blockers (unless waiver) |

## Triggers (description keywords)

Agents match skills via frontmatter `description`. Human triggers:

- “Run preflight”, “requirements first”, “no code yet” → `requirements-engineer`
- “Scaffold docs pack”, “01–09 docs” → `analysis-docs-pack`
- “Spec driven”, “plan before code”, “phased delivery” → `spec-driven-development`
- “Traceability”, “RTM”, “orphan requirements” → `traceability-matrix`
- “Stress test”, “adversarial review”, “red team this” → `adversarial-self-critique`

## File conventions (generic)

| Artifact | Default path |
|----------|--------------|
| Context | `docs/01-context.md` |
| Requirements | `docs/03-requirements.md` |
| Traceability | `docs/08-traceability-matrix.md` |
| Acceptance tests | `docs/09-acceptance-tests.md` |
| Spec | `docs/specs/<slug>.md` |
| Phased plan | `docs/plans/<slug>-plan.md` |
| Phase gate | `docs/plans/<slug>/P<n>.md` |

Projects may relocate paths if `docs/README.md` indexes them.

## Phased delivery

Full loop: [phased-delivery-pipeline.md](phased-delivery-pipeline.md) · Template: `skills/spec-driven-development/templates/phase-gate.md`

## Parked (roadmap)

| Item | Intent |
|------|--------|
| **v0.2 Strategic RE** | Value modeling, stakeholder strategy, long-horizon REQ governance |
| `writing-implementation-plans` | Bite-sized tasks after approved plan |
| `verification-before-completion` | Command output before success claims |
| Orchestrator | Single skill to chain gates with less manual naming |
