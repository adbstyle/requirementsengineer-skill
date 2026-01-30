# User Role Modeling - Zusammenfassung

## Überblick

User Role Modeling ist eine Technik zur Identifikation und Beschreibung verschiedener Benutzertypen, bevor User Stories geschrieben werden. Dies verhindert, dass Stories nur aus der Perspektive eines einzigen Benutzertyps verfasst werden.

## Das Problem

Die meisten Projektteams betrachten nur einen einzigen Benutzertyp beim Schreiben von Stories. Diese Vereinfachung führt zu Software, die die Bedürfnisse wichtiger Benutzergruppen ignoriert.

## Was ist eine User Role?

**User Role** = Eine Sammlung definierender Attribute, die eine Population von Benutzern und deren beabsichtigte Interaktionen mit dem System charakterisieren.

## Der 4-Schritte-Prozess

### 1. Brainstorming initialer User Roles

- Team trifft sich mit Notizenkarten
- Jeder Teilnehmer schreibt so viele Rollennamen wie möglich auf Karten
- Keine Diskussion oder Bewertung während des Brainstormings
- Karten werden ausgelegt, nur der Rollenname wird vorgelesen
- Dauer: ca. 15 Minuten

**Wichtig**: Eine User Role repräsentiert immer einen einzelnen Benutzer, nicht eine Gruppe oder Organisation.

### 2. Organisieren der Rollen

- Karten werden so angeordnet, dass ihre Position die Beziehungen zeigt
- Überlappende Rollen werden überlappend platziert
- Grad der Überlappung zeigt Grad der Ähnlichkeit

### 3. Konsolidieren der Rollen

- Vollständig überlappende Rollen werden zusammengeführt oder eliminiert
- Unwichtige Rollen für den Projekterfolg werden entfernt
- Karten werden neu arrangiert, um Beziehungen zu zeigen
- Generische Rollen können über spezialisierten Versionen positioniert werden

### 4. Verfeinern der Rollen

Attribute für jede Rolle definieren:

- **Nutzungshäufigkeit**: Wie oft wird die Software verwendet?
- **Domain-Expertise**: Fachwissen im Anwendungsbereich
- **Computer-Kenntnisse**: Allgemeine IT-Kompetenz
- **Software-Kenntnisse**: Vertrautheit mit der zu entwickelnden Software
- **Ziele**: Was will der Benutzer erreichen? (Convenience, Rich Experience, etc.)

Notizen zu diesen Attributen werden direkt auf die Rollenkarten geschrieben.

## Beispiel: BigMoneyJobs (Job-Portal)

### Identifizierte Rollen

**Job-Suchende:**
- Job Seeker (allgemein)
- First Timer (Berufseinsteiger)
- Layoff Victim (nach Entlassung)
- Geographic Searcher (ortsspezifische Suche)
- Monitor (gelegentlich am Jobmarkt interessiert)

**Recruiter:**
- Internal Recruiter (für ein Unternehmen)
- External Recruiter (Vermittler)

**System-Verwaltung:**
- Administrator

### Konsolidierung im Beispiel

- College Grad + First Timer → First Timer
- Job Poster + Resume Reader → Recruiter (mit Spezialisierungen)
- Monitor wurde eliminiert (unwichtig für Projekterfolg)

## Zusätzliche Techniken (optional)

### Personas

Eine **Persona** ist eine detaillierte, imaginäre Repräsentation einer User Role:

- Hat einen Namen und eine Hintergrundgeschichte
- Wird mit Foto visualisiert
- Enthält persönliche Details, die sie real erscheinen lassen
- Sollte nur für die 1-2 wichtigsten User Roles erstellt werden

**Beispiel Persona:**
> Mario arbeitet als Recruiter bei SpeedyNetworks. Er ist seit 6 Jahren dort und hat einen Flex-Time-Vertrag mit Home-Office freitags. Mario ist sehr computeraffin und betrachtet sich als Power User. Seine Frau Kim promoviert in Chemie an Stanford. Durch das Wachstum von SpeedyNetworks sucht Mario ständig nach guten Ingenieuren.

**Vorteil**: Stories werden ausdrucksvoller
- Statt: "Ein Benutzer kann Jobsuchen geografisch einschränken"
- Besser: "Ein Geographic Searcher kann seine Jobsuche auf eine bestimmte geografische Region einschränken"

### Extreme Characters

Überzeichnete Charaktere mit extremen Eigenschaften zur Identifikation ungewöhnlicher Requirements.

**Beispiel PDA-Design:**
- Statt nur für Management-Berater zu designen
- Auch für Drug Dealer, den Papst, 20-jährige Frau mit mehreren Freunden

**Nutzen**: Kann zu Stories führen, die sonst übersehen würden (z.B. mehrere separate Kalender für Privatsphäre, größere Schriftarten).

## Einsatz mit On-Site Users

Auch wenn echte Benutzer verfügbar sind, ist User Role Modeling sinnvoll:
- Garantiert nicht, dass die richtigen Benutzer oder die richtige Mischung vorhanden ist
- Hilft sicherzustellen, dass wichtige Benutzergruppen nicht übersehen werden

## Verantwortlichkeiten

### Developer

- Teilnahme am Prozess der Identifikation von User Roles und Personas
- Verständnis jeder User Role/Persona und ihrer Unterschiede
- Während der Entwicklung: Berücksichtigung wie verschiedene Rollen die Software bevorzugen könnten
- Sicherstellen, dass der Prozess nicht über seine Rolle als Werkzeug hinausgeht

### Customer

- Breite Betrachtung möglicher Benutzer und Identifikation geeigneter User Roles
- Teilnahme am Prozess der Identifikation von User Roles und Personas
- Sicherstellen, dass sich die Software nicht unangemessen auf eine Teilmenge von Benutzern fokussiert
- Beim Schreiben von Stories: Sicherstellen, dass jede Story mindestens einer User Role/Persona zugeordnet werden kann
- Während der Entwicklung: Berücksichtigung wie verschiedene Rollen die Software bevorzugen könnten
- Sicherstellen, dass der Prozess nicht über seine Rolle als Werkzeug hinausgeht

## Best Practices

1. **Fokus auf einzelne Benutzer**: Rollen sollten einzelne Personen repräsentieren, nicht Gruppen oder Systeme
2. **System-Rollen vermeiden**: Nur in Ausnahmen nicht-menschliche Rollen definieren
3. **Zeitinvestition**: Ca. 1 Stunde Aufwand bringt mehr Benutzer-Fokus als 99% aller Software-Teams
4. **Selektiver Einsatz**: Personas und Extreme Characters nur nutzen, wenn direkter, greifbarer Nutzen erkennbar ist
5. **Visualisierung**: Role Cards im Team-Bereich aufhängen als ständige Erinnerung

## Nutzen

- Vermeidung von Software, die nur für einen Benutzertyp optimiert ist
- Besseres Verständnis unterschiedlicher Benutzerbedürfnisse
- Ausdrucksstärkere User Stories
- Fokus auf die wichtigsten Benutzergruppen für den Projekterfolg
- Fundierte Basis für Entwicklungsentscheidungen

---

*Basiert auf Kapitel 3 "User Role Modeling" - Konzepte nach Constantine & Lockwood (Usage-Centered Design) und Cooper (Interaction Design)*
