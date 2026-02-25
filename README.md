# Requirements Engineer Plugin

Professional requirements engineering for Claude Code following IREB standards.

## Installation as Plugin (recommended)

### Option 1: Via Marketplace (auto-updates)

```bash
# 1. Marketplace hinzufügen
/plugin marketplace add adbstyle/claude-code-marketplace

# 2. Plugin installieren
/plugin install requirementsengineer@adbstyle-skills
```

### Option 2: Direkt als Plugin (manuell)

```bash
# Plugin installieren (zeigt auf dieses Repo)
/plugin install adbstyle/requirementsengineer-skill
```

### Option 3: In eigene Marketplace einbinden

Andere Marketplace-Betreiber können dieses Plugin in ihrer `marketplace.json` referenzieren:

```json
{
  "plugins": [
    {
      "name": "requirementsengineer",
      "source": {
        "source": "github",
        "repo": "adbstyle/requirementsengineer-skill",
        "ref": "main"
      },
      "description": "Requirements Engineering Skill nach IREB-Standards"
    }
  ]
}
```

Mit `"ref": "main"` wird immer der neueste Stand von `main` gezogen — ohne manuelle Version-Synchronisation.

## Usage

```bash
/requirementsengineer analyse https://jira.example.com/browse/ISSUE-123
/requirementsengineer Als Administrator will ich Rechtegruppen löschen können, damit ich nach unten vererbte Rechte den Organisationen entziehen kann
```

## Features

- Perspective-based validation (Customer, Architect, Tester)
- Natural language format (no GIVEN-WHEN-THEN)
- Compact NFR tables
- Jira integration
- Code context analysis via built-in code-explorer agent

## Structure

```
requirementsengineer-skill/
├── .claude-plugin/
│   └── plugin.json                    # Plugin manifest
├── skills/
│   └── requirementsengineer/
│       ├── SKILL.md                   # Main skill definition
│       ├── agents/
│       │   └── code-explorer.md       # Analyzes codebase for IST-Zustand
│       └── references/               # Reference materials (IREB books, etc.)
└── README.md                          # This file
```

## Subagents

The skill uses two types of subagents via Task tool:

**`general-purpose`** — For parallel data gathering:
- Fetch Jira issues, parent issues, linked issues
- Web searches and document retrieval
- Any fast, parallel information collection

**`requirementsengineer:code-explorer`** — For IST-Zustand analysis:
- Analyzes existing codebase to find constraints
- Identifies where new requirements might conflict
- Documents implicit assumptions in current implementation

No external dependencies required - all functionality is self-contained.

## Author

[@adbstyle](https://github.com/adbstyle)
