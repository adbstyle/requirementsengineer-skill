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

Hypothese
Fuer [Zielgruppe], die [Problem/Beduerfnis], ist [Loesungsbeschreibung] eine Faehigkeit die [erwarteter Nutzen].

Scope
Was gehoert dazu:
1. [Funktionsbereich 1]
2. [Funktionsbereich 2]
3. [Funktionsbereich 3]

Was gehoert NICHT dazu:
1. [Explizite Abgrenzung]

Betroffene Rollen
- [Rolle 1]: [Was diese Rolle tut/braucht]
- [Rolle 2]: [Was diese Rolle tut/braucht]

Vorgeschlagene Story-Zerlegung
1. [Story-Titel] — [1 Satz Beschreibung, welchen End-to-End-Wert diese Story liefert]
2. [Story-Titel] — [1 Satz Beschreibung]
3. [Story-Titel] — [1 Satz Beschreibung]

Erfolgskriterien (Epic-Level)
Woran erkennen wir, dass das Epic erfolgreich umgesetzt ist? Keine AKs, sondern messbare Ergebnisse.
1. [Messbares Ergebnis]
2. [Messbares Ergebnis]

Offene Fragen
1. @[Rolle]: [Frage]
```

## Story-Zerlegung mit SPIDR (Mike Cohn)

Wenn ein Epic in Stories zerlegt werden muss, nutze diese fuenf Dimensionen:

**S — Spike**: Ist noch zu wenig bekannt um Stories zu schreiben? Erst eine Research-Story, dann die eigentlichen Stories.

**P — Paths**: Gibt es verschiedene Wege durch den Workflow? Jeder Pfad kann eine eigene Story sein. Beispiel: "Bezahlung per Kreditkarte" und "Bezahlung per Rechnung".

**I — Interface**: Kann die Anforderung ueber verschiedene Schnittstellen oder Plattformen geliefert werden? Beispiel: "Web-Upload" zuerst, "API-Import" als zweite Story.

**D — Data**: Gibt es Datenvariationen die schrittweise eingefuehrt werden koennen? Beispiel: "Import von Standarddaten" zuerst, "Import mit Sonderfaellen" danach.

**R — Rules**: Koennen Geschaeftsregeln schrittweise eingefuehrt werden? Beispiel: "Standardfall ohne Genehmigung" zuerst, "Sonderfall mit Genehmigungsprozess" danach.

Jede Story muss ein vertikaler Schnitt sein — End-to-End-Wert fuer den User, nicht ein technischer Layer.

## Golden Example: Epic

Marktrückzugsverwaltung

Hypothese
Fuer Regulatory-Affairs-Manager, die Marktrückzuege von Arzneimitteln koordinieren muessen, ist eine digitale Marktrückzugsverwaltung eine Faehigkeit die den Prozess von der Erfassung bis zur behoerdlichen Meldung nachvollziehbar und kontrolliert abbildet.

Scope
Was gehoert dazu:
1. Erfassung und Verwaltung von Marktrückzuegen
2. Statusgesteuerte Prozessabwicklung mit Berechtigungen
3. Dokumentation und Nachvollziehbarkeit aller Entscheidungen

Was gehoert NICHT dazu:
1. Integration mit externen Behoerdensystemen (separates Epic)
2. Automatische Benachrichtigung betroffener Kunden

Betroffene Rollen
- Regulatory-Affairs-Manager: Erfasst Marktrückzuege, steuert den Prozess
- Quality-Manager: Gibt Marktrückzuege frei, trifft Entscheidungen
- Sachbearbeiter: Sieht zugewiesene Marktrückzuege, fuehrt operative Schritte aus

Vorgeschlagene Story-Zerlegung
1. Marktrückzug erfassen — Der RA-Manager kann einen neuen Marktrückzug mit Grunddaten anlegen
2. Marktrückzug-Status verwalten — Berechtigte Rollen koennen den Status entlang definierter Schritte aendern
3. Entscheidfelder bearbeiten — Berechtigte Rollen koennen Entscheidungen dokumentieren und schuetzen
4. Marktrückzug-Aenderungsprotokoll — Alle Statusaenderungen und Entscheidungen sind nachvollziehbar

Erfolgskriterien (Epic-Level)
1. Ein Marktrückzug kann vollstaendig digital von Erfassung bis Abschluss durchlaufen werden
2. Jeder Prozessschritt ist im Aenderungsprotokoll nachvollziehbar
3. Unbefugte Rollen koennen keine Statusaenderungen oder Entscheidungen vornehmen

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess?
2. @Product Owner: Welche Rollen und Berechtigungen muessen abgebildet werden?
3. @Compliance Officer: Gibt es regulatorische Anforderungen an die Aufbewahrungsdauer der Protokolle?
