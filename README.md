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
- Code context analysis

## Updates

```bash
cd ~/.claude/skills/requirementsengineer && git pull
```

## Author

[@adbstyle](https://github.com/adbstyle)
