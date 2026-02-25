# Requirements Engineer Plugin

## Release-Workflow

Wenn Änderungen auf `main` gemergt werden und für andere veröffentlicht werden sollen:

1. Version in `.claude-plugin/plugin.json` bumpen (Semantic Versioning)
2. Version in `marketplace.json` im Repo `adbstyle/claude-code-marketplace` bumpen (gleiche Version)
3. Beide Repos pushen

## Skill bearbeiten

- Skill-Inhalt bearbeiten: `skills/requirementsengineer/SKILL.md` (nicht den Symlink)
- Subagent bearbeiten: `skills/requirementsengineer/agents/code-explorer.md`
- Plugin validieren: `claude plugin validate .`
- Lokales Testen: Änderungen wirken sofort (Symlink), keine Plugin-Installation nötig
- Plugin wird adbstyle **nicht** installiert — nur für andere Nutzer via Marketplace

## Projektstruktur

- **Echte Dateien** liegen unter `skills/requirementsengineer/` (Plugin-Format)
- **Symlinks** auf Root-Ebene (`SKILL.md`, `agents`) ermöglichen lokales Testen ohne Plugin-Install
- Symlinks sind in `.gitignore` und werden nicht committed

## Repos

- **Plugin**: `adbstyle/requirementsengineer-skill`
- **Marketplace**: `adbstyle/claude-code-marketplace`
