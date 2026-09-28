# Changelog

All notable changes to **Preflight** are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [0.1.1] - 2026-09-28

### Added

- [Phased delivery pipeline](docs/phased-delivery-pipeline.md) — Q&A gate → phased plan → per-phase todos → stress-test → human gate → self-improve loop.
- Phase gate template: `skills/spec-driven-development/templates/phase-gate.md`.

### Changed

- `adversarial-self-critique` — ambiguity detection, phase-scoped stress-tests, self-improve hook.
- `spec-driven-development` — deterministic Q&A, phased implementation, per-phase approval gates.
- `requirements-engineer` — constrained clarifying questions; links to phased pipeline.
- GitHub Copilot checklists lightly updated for phased gates (full loop remains Cursor/Claude-native).

### Roadmap (not in this release)

- **v0.2 — Strategic requirements engineering** (value modeling, long-horizon REQ governance).

[0.1.1]: https://github.com/jah-guide/preflight/releases/tag/v0.1.1

## [0.1.0] - 2026-09-28

### Added

- Initial public release: five agent skills for disciplined GenAI delivery.
- `spec-driven-development` — gated specify → plan → implement pipeline.
- `requirements-engineer` — elicitation through testable FRs/NFRs and acceptance criteria.
- `analysis-docs-pack` — scaffold for a numbered `docs/` analysis pack (01–09).
- `traceability-matrix` — REQ → design → test linkage with orphan blocking.
- `adversarial-self-critique` — output stress-test with severity rubric and two revise passes.
- Install guides for Cursor, Claude Code, and GitHub Copilot.
- Thin GitHub Copilot adapter checklists (condensed from full skills).
- Example walkthrough linking to [FlowGate](https://github.com/jah-guide/flowgate).

[0.1.0]: https://github.com/jah-guide/preflight/releases/tag/v0.1.0
