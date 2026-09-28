# Alignment: Preflight skills ↔ 01–09 docs pack

The **analysis-docs-pack** skill scaffolds a numbered documentation set. Other Preflight skills **write into** or **validate** specific files.

## Mapping

| Doc | Primary skill | Secondary |
|-----|---------------|-----------|
| `01-context.md` | `analysis-docs-pack` | `requirements-engineer` (problem statement) |
| `02-stakeholders-raci.md` | `analysis-docs-pack` | `requirements-engineer` (stakeholder map) |
| `03-requirements.md` | `requirements-engineer` | `analysis-docs-pack` (template) |
| `04-use-cases-stories.md` | `analysis-docs-pack` | `requirements-engineer` (scenario validation) |
| `05-process-as-is-to-be.md` | `analysis-docs-pack` | — |
| `06-data-model.md` | `analysis-docs-pack` | `spec-driven-development` (plan detail) |
| `07-sequence-flows.md` | `analysis-docs-pack` | `spec-driven-development` |
| `08-traceability-matrix.md` | `traceability-matrix` | `analysis-docs-pack` (template) |
| `09-acceptance-tests.md` | `analysis-docs-pack` | `traceability-matrix` (coverage) |

## Spec/plan artifacts (optional siblings)

Not part of 01–09 numbering but common alongside:

| Artifact | Skill |
|----------|--------|
| `docs/specs/*.md` | `spec-driven-development` |
| `docs/plans/*-plan.md` | `spec-driven-development` |

## Quality gate across the pack

Before portfolio publish or release:

1. `requirements-engineer` — baseline on `03`  
2. `traceability-matrix` — orphan scan on `08`  
3. `adversarial-self-critique` — stress-test on pack consistency (terminology, ID drift, Must coverage)

## Example reference repo

[FlowGate](https://github.com/jah-guide/flowgate) implements a populated pack under `docs/` — Preflight does **not** fork it; see [examples/flowgate-mini-walkthrough.md](../examples/flowgate-mini-walkthrough.md).
