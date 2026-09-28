# Install Preflight on Claude Code

Claude Code loads skills from user or project skill directories (same `SKILL.md` + frontmatter pattern as Cursor).

## User-wide install

### macOS / Linux

```bash
git clone https://github.com/jah-guide/preflight.git ~/Projects/preflight
mkdir -p ~/.claude/skills
cp -r ~/Projects/preflight/skills/* ~/.claude/skills/
```

### Windows (PowerShell)

```powershell
git clone https://github.com/jah-guide/preflight.git $env:USERPROFILE\Projects\preflight
$dest = "$env:USERPROFILE\.claude\skills"
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item -Recurse -Force "$env:USERPROFILE\Projects\preflight\skills\*" $dest
```

## Project install

Copy selected folders to `.claude/skills/` in the repository.

## Usage

Name the skill in conversation, e.g. “Follow **requirements-engineer** before we write code.”

## Update

Pull Preflight and re-copy, or use symlinks/junctions to `~/Projects/preflight/skills/*`.
