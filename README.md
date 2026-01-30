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

The skill includes a specialized **code-explorer** agent that:
- Analyzes existing codebase implementations (IST-Zustand)
- Identifies extension points for new requirements
- Documents dependencies and architectural patterns
- Provides feasibility assessment for proposed changes

No external dependencies required - all functionality is self-contained.

## Updates

```bash
cd ~/.claude/skills/requirementsengineer && git pull
```

## Author

[@adbstyle](https://github.com/adbstyle)
