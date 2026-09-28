# Install Preflight with GitHub Copilot

Copilot does not load Cursor-style skill folders automatically. Preflight ships **thin adapters** — checklists distilled from full skills.

Location: [`adapters/github-copilot/`](../adapters/github-copilot/)

## What you get

| Adapter | Full skill |
|---------|------------|
| `instructions/requirements-checklist.md` | `requirements-engineer` |
| `instructions/spec-plan-gate.md` | `spec-driven-development` |
| `instructions/docs-pack-checklist.md` | `analysis-docs-pack` |
| `instructions/traceability-checklist.md` | `traceability-matrix` |
| `instructions/stress-test-checklist.md` | `adversarial-self-critique` |

Each file is ≤80 lines.

## Wiring (repository)

1. Copy desired files into `.github/copilot-instructions.md` **or** merge sections from `adapters/github-copilot/instructions/` into your existing Copilot instructions file.
2. For org-wide policy, use your org’s Copilot custom instructions mechanism (enterprise) or document the checklist in `CONTRIBUTING.md`.

## Wiring (VS Code workspace)

Add to `.vscode/settings.json` if your Copilot version supports custom instructions path — point at a merged markdown file that `@include`s the checklists.

## Limitations (explicit)

- **No automatic two-pass adversarial loop** — run the stress-test checklist manually or ask Copilot to produce one critique table per turn.
- **Gates are honor-system** — human must reject “jump to code” responses.
- For full gates and revise passes, use Cursor or Claude Code with native skills.

## One-liner clone

```bash
git clone https://github.com/jah-guide/preflight.git
```

Then copy checklists from `preflight/adapters/github-copilot/instructions/`.
