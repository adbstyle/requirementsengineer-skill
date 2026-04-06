# Epic vs. User Story

Lies diese Referenz, wenn du unsicher bist ob der Input ein Epic oder eine Story ist, oder wenn du ein Epic dokumentieren sollst.

## Definition (nach Mike Cohn)

Ein Epic ist einfach eine grosse User Story — es gibt keine magische Schwelle. Der Begriff kommt aus XP und beschreibt eine Anforderung, die zu gross ist um in einem Sprint umgesetzt zu werden. Sobald ein Epic in die Nähe der Umsetzung rückt, wird es in mehrere kleine Stories zerlegt.

## Wann ist etwas ein Epic?

Prüfe diese Indikatoren:
- Mehrere unabhängige Workflows in einer Anforderung (Erstellen + Bearbeiten + Löschen + Importieren + Berechtigungen)
- Mehrere Rollen mit unterschiedlichen Interaktionen
- Umsetzung würde realistisch mehrere Sprints dauern
- Das Ticket oder der User spricht explizit von "Epic" oder "Feature"
- Die Anforderung beschreibt ein Themengebiet, nicht eine einzelne Interaktion

Wenn keiner dieser Indikatoren zutrifft, ist es eine Story.

## Unterschiedlicher Output je nach Ebene

### Story-Level (Standard)
Detaillierte Dokumentation mit allen Sektionen: Story-Skelett, Preconditions, Acceptance Criteria, Postconditions, Out of Scope, Offene Fragen. Jedes AK ist ein vollständiger, testbarer Satz. Siehe `references/golden-example.md`.

### Epic-Level
Grobgranulare Dokumentation — ein Epic bekommt KEINE 20 detaillierten AKs. Stattdessen:

```
[Epic-Name]

Als [Zielgruppe/Rolle]
möchte ich [Ziel/Wunsch auf Epic-Ebene]
damit [Geschäftswert/Nutzen]

Preconditions
1. [Zustand oder Voraussetzung, die vor Start des Epics gegeben sein muss]

In Scope
1. [Funktionsbereich 1]
2. [Funktionsbereich 2]
3. [Funktionsbereich 3]

Erfolgskriterien
1. [Messbares Ergebnis, woran erkennt wird, dass das Epic erfolgreich war]
2. [Messbares Ergebnis, woran erkennt wird, dass das Epic erfolgreich war]

Out of Scope
1. [Aussagesatz der beschreibt, was das System NICHT tut — auch ohne Überschrift verständlich]

Offene Fragen
1. @[Rolle]: [Frage]
```

## Golden Example: Epic

Marktrückzugsverwaltung

Als Regulatory-Affairs-Manager
möchte ich Marktrückzüge von Arzneimitteln digital erfassen und entlang eines definierten Prozesses steuern können
damit der Rückzugsprozess von der Erfassung bis zur behördlichen Meldung nachvollziehbar und kontrolliert abläuft

Preconditions
1. Ein Rollen- und Berechtigungskonzept für Regulatory Affairs ist im System vorhanden
2. Die relevanten Arzneimittel sind im Stammdatensystem erfasst

In Scope
1. Erfassung und Verwaltung von Marktrückzügen
2. Statusgesteuerte Prozessabwicklung mit Berechtigungen
3. Dokumentation und Nachvollziehbarkeit aller Entscheidungen

Erfolgskriterien
1. Ein Marktrückzug kann vollständig digital von Erfassung bis Abschluss durchlaufen werden
2. Jeder Prozessschritt ist im Änderungsprotokoll nachvollziehbar
3. Unbefugte Rollen können keine Statusänderungen oder Entscheidungen vornehmen

Out of Scope
1. Das SYSTEM kommuniziert nicht direkt mit externen Behördensystemen
2. Das SYSTEM versendet keine automatischen Benachrichtigungen an betroffene Kunden

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess?
2. @Product Owner: Welche Rollen und Berechtigungen müssen abgebildet werden?
3. @Compliance Officer: Gibt es regulatorische Anforderungen an die Aufbewahrungsdauer der Protokolle?
