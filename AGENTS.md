# Agent instructions (Preflight)

This repository ships **Cursor** and **Claude Code** skills under `skills/<id>/SKILL.md`.

**GitHub Copilot:** use `adapters/github-copilot/` — condensed checklists, not full skill bodies. See [docs/install-github-copilot.md](docs/install-github-copilot.md).

**Recommended order for greenfield work:**

1. `requirements-engineer` — deterministic Q&A, problem statement, FRs/NFRs, AC (no implementation yet).
2. `analysis-docs-pack` — materialize the 01–09 docs pack when the initiative needs analyst-grade artifacts.
3. `spec-driven-development` — Q&A → phased plan → per-phase todos → stress-test → **human gate between phases**; plan approval before code.
4. `traceability-matrix` — keep REQ → design → test aligned; block “done” on orphans.
5. `adversarial-self-critique` — phase-scoped and final stress-tests before ship (max two revise passes).

**Self-improve:** on repeat mistakes, propose concrete `SKILL.md` or `lessons.md` edits to the human — do not auto-commit to this repo unless asked.

Phased workflow: [docs/phased-delivery-pipeline.md](docs/phased-delivery-pipeline.md) · Full map: [docs/skill-map.md](docs/skill-map.md).
