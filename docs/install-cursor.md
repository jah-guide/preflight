# Install Preflight on Cursor

Preflight skills are folders with a `SKILL.md` file. Cursor discovers them from skill paths configured in your environment.

## Recommended: personal skills

Works across all projects.

### Windows (PowerShell)

```powershell
git clone https://github.com/jah-guide/preflight.git $env:USERPROFILE\Projects\preflight
$dest = "$env:USERPROFILE\.cursor\skills"
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item -Recurse -Force "$env:USERPROFILE\Projects\preflight\skills\*" $dest
```

### macOS / Linux

```bash
git clone https://github.com/jah-guide/preflight.git ~/Projects/preflight
mkdir -p ~/.cursor/skills
cp -r ~/Projects/preflight/skills/* ~/.cursor/skills/
```

## Project-scoped skills

For a single repo, copy into `.cursor/skills/` at the project root and commit if the team shares them.

## Verify

In Agent chat, ask to use **`spec-driven-development`** on a hypothetical feature — the agent should refuse to implement before plan approval.

## Update

```bash
cd ~/Projects/preflight && git pull
# re-copy or symlink skills into ~/.cursor/skills/
```

**Do not** copy into `~/.cursor/skills-cursor/` — reserved for Cursor built-ins.
