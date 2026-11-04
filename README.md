# Requirements Engineer Plugin

Professional requirements engineering for Claude Code following IREB standards.

## Installation as Plugin (recommended)

```bash
# 1. Marketplace hinzufügen
/plugin marketplace add adbstyle/claude-code-marketplace

# 2. Plugin installieren
/plugin install requirementsengineer@adbstyle-skills
```

### Updates automatisch erhalten

Auto-Update ist für Marketplaces von Drittanbietern standardmässig aus. Einmal einschalten: `/plugin` → Marketplaces → `adbstyle-skills` → «Enable auto-update». Claude Code prüft dann in jeder Session auf eine neue Version.

Eine neue Version erkennt Claude Code an `version` in `.claude-plugin/plugin.json`. Neue Stände kommen deshalb mit jedem Release, nicht mit jedem Commit.

### In eine eigene Marketplace einbinden

Andere Marketplace-Betreiber können dieses Plugin in ihrer `marketplace.json` referenzieren:

```json
{
  "plugins": [
    {
      "name": "requirementsengineer",
      "source": {
        "source": "github",
        "repo": "adbstyle/requirementsengineer-skill"
      },
      "description": "Requirements Engineering Skill nach IREB-Standards"
    }
  ]
}
```

Ohne `ref` zieht Claude Code den Default-Branch `main`, auf dem nur Releases landen. Eine `version` im Marketplace-Eintrag ist nicht nötig, denn `version` aus `plugin.json` hat Vorrang.

### Als persönlicher Skill (ohne Plugin)

Den Ordner `skills/requirementsengineer` nach `~/.claude/skills/requirementsengineer` kopieren oder verlinken. Der Skill läuft dann ohne den Plugin-Agenten `code-explorer`: Für die Codebase-Analyse nimmt er einen `general-purpose`-Agenten mit derselben Anleitung. Updates kommen nicht automatisch.

## Usage

Der Skill startet von selbst, sobald es um Anforderungen, User Stories oder Akzeptanzkriterien geht. Direkt aufrufen:

```bash
/requirementsengineer:requirementsengineer analysiere https://jira.example.com/browse/ISSUE-123
/requirementsengineer:requirementsengineer Als Administrator will ich Rechtegruppen löschen können, damit ich nach unten vererbte Rechte den Organisationen entziehen kann
```

Als persönlicher Skill heisst der Befehl `/requirementsengineer`.

## Features

- Workflow in Phasen mit Aufgabenliste: Discovery, Kontext (Tracker, Dokumente, Codebase), Dokumentation, Validierung, auf Auftrag Rückschreiben in den Tracker
- Epic oder Story, Business oder Enabler, Story-Schnitt nach SPIDR
- Verbindliche Struktur nach Golden Example: Story-Satz, Preconditions, Acceptance Criteria, Postconditions, Out of Scope, Offene Fragen
- Drei Prüfungen für jeden Satz: Notwendigkeit, Eine Regel ein Satz, Austauschbarkeit
- Perspektivenbasiertes Lesen mit sechs Perspektiven (Kunde, Architekt, Tester, Business Analyst, Fachexperte, UX) plus Regel-Prüfer
- Rückfragen interaktiv, sobald sie entstehen
- Rückschreiben in den Tracker mit minimalem Diff: Im Änderungsprotokoll erscheinen nur die geänderten Zeilen
- Unabhängig vom Tracker: Jira, GitHub Issues, Linear, Azure DevOps und andere, über MCP, CLI oder API
- Natürliche Sprache statt GIVEN-WHEN-THEN, NFRs als nummerierte Sätze

## Structure

```
requirementsengineer-skill/
├── .claude-plugin/
│   └── plugin.json                       # Plugin-Manifest, registriert den code-explorer
├── skills/
│   └── requirementsengineer/
│       ├── SKILL.md                      # Skill-Definition und Workflow
│       ├── agents/
│       │   └── code-explorer.md          # Codebase-Analyse für den IST-Zustand
│       └── references/
│           ├── golden-example.md         # Verbindliche Story-Struktur
│           ├── anti-patterns.md          # Checkliste für Schreiben und Regel-Prüfer
│           ├── epic-vs-story.md          # Epic vs. Story, Business vs. Enabler, Erfolgskriterien
│           ├── validation-house-rules.md # Hausregeln für die Validierungsagenten
│           ├── tracker-writeback.md      # Regeln für das Rückschreiben
│           ├── INVEST-Prinzip-Zusammenfassung.md
│           └── User-Role-Modeling-Zusammenfassung.md
├── feedback/
│   └── FEEDBACK-LOG.md                   # Gesammeltes Feedback, wird vom Skill nicht geladen
└── README.md
```

## Subagents

Der Skill startet Subagenten über das Subagent-Tool des Harness (`Agent`, in älteren Versionen `Task`):

**`general-purpose`**
- Phase 2: Kontext aus Issue, Parent, verlinkten Issues und Dokumenten sammeln
- Phase 4: perspektivenbasiertes Lesen mit sechs Perspektiven und Regel-Prüfer

**`requirementsengineer:code-explorer`**
- Phase 2: IST-Analyse der Codebase
- Findet Einschränkungen, Konflikte mit neuen Anforderungen und implizite Annahmen
- Registriert über `plugin.json`. Ohne Plugin-Installation übernimmt ein `general-purpose`-Agent mit derselben Anleitung.

Für den Tracker-Kontext nutzt der Skill, was in der Session verfügbar ist: MCP-Tools, eine CLI wie `gh` oder `jira`, oder die REST-API.

## Author

[@adbstyle](https://github.com/adbstyle)
