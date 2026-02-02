# Requirements Engineer Skill

Professional requirements engineering for Claude Code following IREB standards.

## Installation

```bash
cd ~/.claude/skills
git clone https://github.com/adbstyle/requirementsengineer-skill.git requirementsengineer
```

## Usage

```bash
claude /requirementsengineer analyse https://jira.example.com/browse/ISSUE-123
claude /requirementsengineer Als Administartor will ich Rechtegruppen löschen können, damit ich nach unten vererbte Rechte den Organisationen entziehen kann
```

## Features

- Perspective-based validation (Customer, Architect, Tester)
- Natural language format (no GIVEN-WHEN-THEN)
- Compact NFR tables
- Jira integration
- Code context analysis via built-in code-explorer agent

## Structure

```
requirementsengineer/
├── SKILL.md           # Main skill definition
├── README.md          # This file
├── agents/            # Subagents
│   └── code-explorer.md  # Analyzes codebase for IST-Zustand
└── references/        # Reference materials (IREB books, etc.)
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

## Updates

```bash
cd ~/.claude/skills/requirementsengineer && git pull
```

## Author

[@adbstyle](https://github.com/adbstyle)
