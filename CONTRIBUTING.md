# Contributing to Preflight

Thank you for improving agent skills for disciplined delivery.

## What belongs here

- **Skills** under `skills/<id>/SKILL.md` — Cursor/Claude-compatible, YAML frontmatter, third-person `description`
- **Templates** beside skills when progressive disclosure helps
- **Copilot adapters** under `adapters/github-copilot/` — thin checklists (≤80 lines each), not duplicates of full skills
- **Docs** under `docs/` — install guides, maps, credential one-pagers

## Skill quality bar

1. **Name** — lowercase, hyphens, matches folder id  
2. **Description** — WHAT + WHEN triggers, third person, under 1024 chars  
3. **Body** — actionable gates, tables, anti-patterns; prefer &lt;500 lines  
4. **No secret sauce** — no API keys, private URLs, or employer-locked paths  
5. **Honest scope** — if Copilot cannot run multi-pass critique, say so in adapter

## Pull request checklist

- [ ] Skill discovery description updated if behavior changed
- [ ] `docs/skill-map.md` updated if adding/removing skills
- [ ] `CHANGELOG.md` entry under Unreleased or next version
- [ ] Copilot adapter added/updated for new skills

## Development

Fork → branch → PR. MIT licensed contributions welcome.

## Code of conduct

Be direct, evidence-based, and respectful. Preflight skills model the same tone: challenge ideas, not people.
