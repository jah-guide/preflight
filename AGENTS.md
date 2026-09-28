# Agent instructions (Preflight)

This repository ships **Cursor** and **Claude Code** skills under `skills/<id>/SKILL.md`.

**GitHub Copilot:** use `adapters/github-copilot/` — condensed checklists, not full skill bodies. See [docs/install-github-copilot.md](docs/install-github-copilot.md).

**Recommended order for greenfield work:**

1. `requirements-engineer` — problem statement, FRs/NFRs, AC (no implementation yet).
2. `analysis-docs-pack` — materialize the 01–09 docs pack when the initiative needs analyst-grade artifacts.
3. `spec-driven-development` — gate design/plan approval before code.
4. `traceability-matrix` — keep REQ → design → test aligned; block “done” on orphans.
5. `adversarial-self-critique` — stress-test outputs before ship (max two revise passes).

Full map: [docs/skill-map.md](docs/skill-map.md).
