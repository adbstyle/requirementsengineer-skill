# Epic vs. User Story

Lies diese Referenz, wenn du unsicher bist ob der Input ein Epic oder eine Story ist, oder wenn du ein Epic dokumentieren sollst.

## Definition (nach Mike Cohn)

Ein Epic ist einfach eine grosse User Story — es gibt keine magische Schwelle. Der Begriff kommt aus XP und beschreibt eine Anforderung, die zu gross ist um in einem Sprint umgesetzt zu werden. Sobald ein Epic in die Naehe der Umsetzung rueckt, wird es in mehrere kleine Stories zerlegt.

## Wann ist etwas ein Epic?

Pruefe diese Indikatoren:
- Mehrere unabhaengige Workflows in einer Anforderung (Erstellen + Bearbeiten + Loeschen + Importieren + Berechtigungen)
- Mehrere Rollen mit unterschiedlichen Interaktionen
- Umsetzung wuerde realistisch mehrere Sprints dauern
- Das Ticket oder der User spricht explizit von "Epic" oder "Feature"
- Die Anforderung beschreibt ein Themengebiet, nicht eine einzelne Interaktion

Wenn keiner dieser Indikatoren zutrifft, ist es eine Story.

## Unterschiedlicher Output je nach Ebene

### Story-Level (Standard)
Detaillierte Dokumentation mit allen Sektionen: Story-Skelett, Preconditions, Acceptance Criteria, Postconditions, Out of Scope, Offene Fragen. Jedes AK ist ein vollstaendiger, testbarer Satz. Siehe `references/golden-example.md`.

### Epic-Level
Grobgranulare Dokumentation — ein Epic bekommt KEINE 20 detaillierten AKs. Stattdessen:

```
[Epic-Name]

Als [Zielgruppe/Rolle]
moechte ich [Ziel/Wunsch auf Epic-Ebene]
damit [Geschaeftswert/Nutzen]

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
1. [Explizite Abgrenzung 1]
2. [Explizite Abgrenzung 2]
3. [Explizite Abgrenzung 3]

Offene Fragen
1. @[Rolle]: [Frage]
```

## Golden Example: Epic

Marktrückzugsverwaltung

Als Regulatory-Affairs-Manager
moechte ich Marktrückzuege von Arzneimitteln digital erfassen und entlang eines definierten Prozesses steuern koennen
damit der Rückzugsprozess von der Erfassung bis zur behoerdlichen Meldung nachvollziehbar und kontrolliert ablaeuft

Preconditions
1. Ein Rollen- und Berechtigungskonzept fuer Regulatory Affairs ist im System vorhanden
2. Die relevanten Arzneimittel sind im Stammdatensystem erfasst

In Scope
1. Erfassung und Verwaltung von Marktrückzuegen
2. Statusgesteuerte Prozessabwicklung mit Berechtigungen
3. Dokumentation und Nachvollziehbarkeit aller Entscheidungen

Erfolgskriterien
1. Ein Marktrückzug kann vollstaendig digital von Erfassung bis Abschluss durchlaufen werden
2. Jeder Prozessschritt ist im Aenderungsprotokoll nachvollziehbar
3. Unbefugte Rollen koennen keine Statusaenderungen oder Entscheidungen vornehmen

Out of Scope
1. Integration mit externen Behoerdensystemen (separates Epic)
2. Automatische Benachrichtigung betroffener Kunden

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess?
2. @Product Owner: Welche Rollen und Berechtigungen muessen abgebildet werden?
3. @Compliance Officer: Gibt es regulatorische Anforderungen an die Aufbewahrungsdauer der Protokolle?
