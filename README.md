# Preflight

**Agent skills that force requirements, traceability, and adversarial stress-tests before AI ships an answer.**

GenAI coding agents are fast — Preflight makes them **disciplined**: elicit real problems, document testable requirements, scaffold analyst-grade docs, keep REQ → design → test aligned, and stress-test outputs before “done.”

Repository: [github.com/jah-guide/preflight](https://github.com/jah-guide/preflight)

---

## Why Preflight exists

Most agent failures are not syntax errors. They are **wrong problem, missing edge cases, untested Must-haves, and confident claims without evidence**. Preflight encodes the same gates a strong systems analyst uses before implementation — as skills your agent can load on demand.

**Design first. Build once.** Same motto as [jah-guide](https://github.com/jah-guide)'s portfolio work ([FlowGate](https://github.com/jah-guide/flowgate), [SourceMap](https://github.com/jah-guide/sourcemap)).

---

## Skills (v0.1)

| Skill | Role |
|-------|------|
| [`requirements-engineer`](skills/requirements-engineer/SKILL.md) | Full RE loop + **no code until problem & Must FRs exist** |
| [`analysis-docs-pack`](skills/analysis-docs-pack/SKILL.md) | Scaffold generic `docs/01`–`09` analysis pack |
| [`spec-driven-development`](skills/spec-driven-development/SKILL.md) | Gated specify → plan → implement; **no code until plan approved** |
| [`traceability-matrix`](skills/traceability-matrix/SKILL.md) | REQ → design → test; **block done on orphans** |
| [`adversarial-self-critique`](skills/adversarial-self-critique/SKILL.md) | **Output stress-test** — severity rubric, max 2 revise passes, stress-tested note |

Suggested flow: **requirements-engineer → analysis-docs-pack → spec-driven-development → (implement) → traceability-matrix → adversarial-self-critique**

Map and triggers: [docs/skill-map.md](docs/skill-map.md)

---

## Install matrix

| Environment | Guide | One-liner |
|-------------|-------|-----------|
| **Cursor** | [docs/install-cursor.md](docs/install-cursor.md) | Clone into `~/.cursor/skills/` or symlink each `skills/<id>` |
| **Claude Code** | [docs/install-claude-code.md](docs/install-claude-code.md) | Clone into `~/.claude/skills/` (or project `.claude/skills/`) |
| **GitHub Copilot** | [docs/install-github-copilot.md](docs/install-github-copilot.md) | Copy `adapters/github-copilot/instructions/*.md` — **checklists only** |

### Cursor (quick)

```bash
git clone https://github.com/jah-guide/preflight.git
# Option A — whole pack
cp -r preflight/skills/* ~/.cursor/skills/
# Option B — one skill
cp -r preflight/skills/spec-driven-development ~/.cursor/skills/
```

### Claude Code (quick)

```bash
git clone https://github.com/jah-guide/preflight.git
cp -r preflight/skills/* ~/.claude/skills/
```

### GitHub Copilot (quick)

```bash
git clone https://github.com/jah-guide/preflight.git
# Follow docs/install-github-copilot.md to wire instructions/*.md
```

---

## Honest note on GitHub Copilot

**Full multi-pass adversarial critique and gated pipelines are Cursor/Claude-native** — agents can load skills, iterate, and hold gates across turns.

Copilot adapters in [`adapters/github-copilot/`](adapters/github-copilot/) are **condensed checklists** (≤80 lines each). They remind; they do not replace deep skill bodies. See [AGENTS.md](AGENTS.md).

---

## Docs & credential one-pager

- [GenAI disciplined delivery (1-pager)](docs/genai-disciplined-delivery.md) — badge / credential narrative  
- [Alignment with the 01–09 docs pack](docs/alignment-with-docs-pack.md)  
- [FlowGate mini walkthrough (links out)](examples/flowgate-mini-walkthrough.md)

---

## Roadmap (parked)

Not in v0.1 — planned later:

- `writing-implementation-plans` — task-level plans after spec approval  
- `verification-before-completion` — evidence-before-claims iron law  
- **Orchestrator skill** — single entry skill chaining Preflight gates (heavy; needs dogfooding)

Track via [CHANGELOG.md](CHANGELOG.md) and GitHub issues.

---

## License

MIT — see [LICENSE](LICENSE).

## Author

Maintained by [@jah-guide](https://github.com/jah-guide) (Bohlokoa) — systems analyst & engineer portfolio.
