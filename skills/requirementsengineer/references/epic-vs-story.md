# Ebene und Typ: Die zwei Dimensionen einer Anforderung

Lies diese Referenz, wenn du unsicher bist ob der Input ein Epic oder eine Story ist, ob es ein Business- oder Enabler-Element ist, oder wenn du ein Epic dokumentieren sollst.

Jede Anforderung hat zwei unabhängige Dimensionen:
- **Ebene**: Epic (zu gross für einen Sprint) vs. Story (passt in einen Sprint)
- **Typ**: Business (liefert direkten Nutzerwert) vs. Enabler (schafft technische Voraussetzungen)

Diese Kombination ergibt vier mögliche Formen: Business Epic, Enabler Epic, User Story (Business), Enabler Story.

## Ebene: Epic vs. Story

### Definition (nach Mike Cohn)

Ein Epic ist einfach eine grosse User Story — es gibt keine magische Schwelle. Der Begriff kommt aus XP und beschreibt eine Anforderung, die zu gross ist um in einem Sprint umgesetzt zu werden. Sobald ein Epic in die Nähe der Umsetzung rückt, wird es in mehrere kleine Stories zerlegt.

### Wann ist etwas ein Epic?

Prüfe diese Indikatoren:
- Mehrere unabhängige Workflows in einer Anforderung (Erstellen + Bearbeiten + Löschen + Importieren + Berechtigungen)
- Mehrere Rollen mit unterschiedlichen Interaktionen
- Umsetzung würde realistisch mehrere Sprints dauern
- Das Ticket oder der User spricht explizit von "Epic" oder "Feature"
- Die Anforderung beschreibt ein Themengebiet, nicht eine einzelne Interaktion

Wenn keiner dieser Indikatoren zutrifft, ist es eine Story.

## Typ: Business vs. Enabler

Die Unterscheidung zwischen Business- und Enabler-Elementen (nach SAFe, Knaster/Leffingwell) gilt auf beiden Ebenen — Epic und Story. Der Typ bestimmt, wer der Akteur ist, wie die Erfolgskriterien bzw. Acceptance Criteria formuliert werden und was "fertig" bedeutet.

### Business (Epic oder Story)

Liefert direkt Wert für den Endnutzer — neue Funktionalität, ein neuer Prozess, eine Verbesserung des bestehenden Systems. Der Erfolg zeigt sich daran, dass sich etwas im Verhalten oder in der Erfahrung des Nutzers ändert.

Erkennungsmerkmale:
- Beschreibt eine Nutzer-Interaktion oder einen Geschäftsprozess
- Der Endnutzer ist direkt betroffen
- Das Story-Skelett beginnt mit einer fachlichen Rolle ("Als Sachbearbeiter", "Als Regulatory-Affairs-Manager")

### Enabler (Epic oder Story)

Schafft Voraussetzungen für zukünftige Business-Elemente — baut die "Architectural Runway" (Architektur-Basis) aus, damit zukünftige Business-Features effizient und stabil ausgeliefert werden können. Der Endnutzer merkt direkt nichts davon.

Typische Enabler-Kategorien:
- **Exploration** — Analysen, Evaluationen, Spike/Proof of Concept
- **Architektur** — Datenmodelle, API-Design, Schnittstellen-Spezifikation
- **Infrastruktur** — Projekt-Scaffolding, CI/CD, Monitoring
- **Refactoring** — Technische Schulden abbauen, Modularisierung
- **Compliance** — Regulatorische Grundlagen, Audit-Fähigkeit

Erkennungsmerkmale:
- Beschreibt eine Analyse, Evaluation, technische Grundlagenarbeit oder Infrastruktur-Aufbau
- Das Ergebnis ist ein Artefakt (Dokument, Entscheid, Prototyp) oder eine technische Grundlage, kein nutzbares Feature
- Das Story-Skelett beginnt oft mit einer technischen oder organisatorischen Rolle ("Als Entwicklungsteam", "Als Architekt")

## Unterschiedlicher Output je nach Ebene und Typ

### Story-Level: User Story (Business)
Detaillierte Dokumentation mit allen Sektionen: Story-Skelett, Preconditions, Acceptance Criteria, Postconditions, Out of Scope, Offene Fragen. Jedes AK ist ein vollständiger, testbarer Satz. Der USER ist der aktive Akteur. Siehe `references/golden-example.md`.

### Story-Level: Enabler Story
Gleiche Sektionen wie eine User Story, aber mit angepasstem Akteur und Fokus:
- **Story-Skelett**: Die Rolle ist technisch/organisatorisch ("Als Entwicklungsteam", "Als DevOps-Engineer"), nicht der Endnutzer
- **Acceptance Criteria**: Beschreiben technische Ergebnisse oder Entscheide, nicht Nutzer-Interaktionen. Der Akteur ist das TEAM oder das SYSTEM, nicht der USER. AKs bleiben testbar, aber die Testbarkeit bezieht sich auf technische Nachweise, nicht auf Nutzer-Verhalten.
- **Postconditions**: System-Zustände, die nach Abschluss gelten (z.B. "Die CI-Pipeline läuft grün durch", "Das Schema ist in der Staging-Umgebung deployt")

Statt (User Story Pattern auf Enabler-Arbeit gezwungen):
  Als Sachbearbeiter möchte ich, dass die Datenbank-Migration durchgeführt wird
Richtig (Enabler Story mit technischer Rolle):
  Als Entwicklungsteam möchte ich das Datenbankschema auf die neue Domänenstruktur migrieren, damit die nachfolgenden Business Stories auf einem konsistenten Datenmodell aufbauen können

Statt (USER als Akteur bei technischer Arbeit):
  1. Der USER kann die API aufrufen
Richtig (TEAM/SYSTEM als Akteur):
  1. Das SYSTEM stellt einen REST-Endpunkt bereit, der das MHP-Datenformat gemäss dem dokumentierten Schema zurückgibt
  2. Das TEAM hat die Mapping-Regeln als automatisierte Transformationslogik implementiert, die alle Pflichtfelder abdeckt

Siehe `references/golden-example.md` für ein vollständiges Enabler-Story-Beispiel.

### Epic-Level
Grobgranulare Dokumentation — ein Epic bekommt KEINE 20 detaillierten AKs. Stattdessen:

```
[Epic-Name]

Als [Zielgruppe/Rolle]
möchte ich [Ziel/Wunsch auf Epic-Ebene]
damit [Geschäftswert/Nutzen]

Preconditions
1. [Zustand oder Voraussetzung, die vor Start des Epics gegeben sein muss]

Erfolgskriterien
1. [Selbst-verifizierendes Outcome — siehe Formulierungsregeln unten]

Out of Scope
1. [Aussagesatz der beschreibt, was bewusst nicht Teil dieses Epics ist — auch ohne Überschrift verständlich]

Offene Fragen
1. @[Rolle]: [Frage]
```

### Warum kein "In Scope"?

Ein Epic hat keine separate "In Scope"-Sektion. Der Scope ergibt sich implizit aus zwei Quellen:
- Das **Story-Skelett** ("Als... möchte ich... damit...") definiert das Ziel und den Rahmen
- Die **Erfolgskriterien** definieren die überprüfbaren Ergebnisse — was am Ende vorliegen muss

Eine zusätzliche "In Scope"-Liste wäre redundant: Sie beschreibt die gleichen Themen, die die Erfolgskriterien bereits schärfer und testbar formulieren. Wenn ein Thema kein eigenes Erfolgskriterium rechtfertigt, ist es entweder Teil eines übergreifenden Ergebniskriteriums oder es gehört nicht ins Epic.

Die Grenzziehung übernimmt **Out of Scope** — dort steht explizit, was bewusst ausgeschlossen ist und wo Scope Creep droht.

## Erfolgskriterien auf Epic-Ebene

Erfolgskriterien auf Epic-Ebene sind die Messlatte für die Abnahme. Sie müssen zwei Anforderungen gleichzeitig erfüllen:
- **Outcome-orientiert** — sie beschreiben, was sich für den Nutzer oder das Business ändert, nicht welches Feature existiert
- **Selbst-verifizierend** — die Formulierung ist so spezifisch, dass ein Stakeholder beim Lesen sofort weiss, was er prüfen müsste, ohne dass das Kriterium eine Verifikationsmethode vorschreibt

Die Verifikationsmethode (wie genau geprüft wird) entsteht später — auf Story-Ebene in den Acceptance Criteria oder im Testkonzept. Zum Zeitpunkt der Epic-Formulierung ist der Weg zur Umsetzung noch zu unklar, um Verifikation festzulegen.

### Formulierungsregel: Spezifität statt Verifikation

Der Schlüssel zu selbst-verifizierenden Kriterien liegt in der Spezifität des Outcomes. Vage Kriterien brauchen eine Verifikationsmethode als Krücke. Spezifische Kriterien sind aus sich selbst heraus prüfbar.

Statt (vage — braucht Verifikationsmethode):
  "Der Prozess ist digital"
  "Das System ist nachvollziehbar"
  "Berechtigungen funktionieren"
Richtig (spezifisch — selbst-verifizierend):
  "Kein Prozessschritt erfordert ein Medium ausserhalb des Systems"
  "Jeder Statusübergang ist mit Zeitpunkt, User und vorherigem Status rekonstruierbar"
  "Kein User kann Aktionen ausführen, die seine Rolle nicht vorsieht"

**Litmus-Test:** Wenn ein Stakeholder das Erfolgskriterium liest und nicht weiss, was er prüfen müsste, ist es zu vage. Wenn er es liest und sofort eine Idee hat wie er es prüfen würde — auch ohne explizite Verifikationsmethode — ist es gut formuliert.

### Erfolgskriterien bei Epics (Business Epics)

Erfolgskriterien beschreiben, was sich für den Nutzer ändert — das beobachtbare Outcome, nicht das technische Artefakt.

Statt (Output-orientiert — Feature existiert):
  "Das System kann Marktrückzüge verwalten"
  "Ein Dashboard zeigt den Prozessstatus an"
Richtig (Outcome-orientiert — Nutzer-Erfahrung ändert sich):
  "Ein Marktrückzug kann vollständig digital von Erfassung bis Abschluss durchlaufen werden, ohne dass ein Schritt ausserhalb des Systems erfolgt"
  "Der aktuelle Status jedes Marktrückzugs ist für berechtigte Rollen jederzeit einsehbar, ohne Rückfrage an andere Personen"

### Erfolgskriterien bei Enabler Epics

Bei Enabler Epics IST das Artefakt das Outcome — ein Analysedokument, ein Entscheid, ein Mapping. Output und Outcome fallen zusammen. Die Spezifität kommt hier aus dem Qualitätsniveau des Artefakts.

Statt (vage — "es liegt vor"):
  "Ein Mapping der swissdamed-Daten liegt vor"
  "Die Produktidentifikation ist geklärt"
Richtig (spezifisch — Qualitätsniveau definiert):
  "Für jedes swissdamed-Pflichtfeld ist dokumentiert, ob es ins MHP-Zieldatenformat übernommen, transformiert oder ignoriert wird, inklusive Begründung"
  "Die Produktidentifikation ist als Entscheidungsdokument festgehalten mit Begründung, warum der gewählte Schlüssel gegenüber Alternativen bevorzugt wird"

## Golden Example: Epic (Business Epic)

Marktrückzugsverwaltung

Als Regulatory-Affairs-Manager
möchte ich Marktrückzüge von Arzneimitteln digital erfassen und entlang eines definierten Prozesses steuern können
damit der Rückzugsprozess von der Erfassung bis zur behördlichen Meldung nachvollziehbar und kontrolliert abläuft

Preconditions
1. Ein Rollen- und Berechtigungskonzept für Regulatory Affairs ist im System vorhanden
2. Die relevanten Arzneimittel sind im Stammdatensystem erfasst

Erfolgskriterien
1. Ein Marktrückzug kann vollständig digital von Erfassung bis Abschluss durchlaufen werden, ohne dass ein Schritt ausserhalb des Systems erfolgt
2. Jeder Statusübergang ist mit Zeitpunkt, ausführendem User und vorherigem Status rekonstruierbar
3. Kein User kann Statusänderungen oder Entscheidungen vornehmen, die seine Rolle nicht vorsieht

Out of Scope
1. Das SYSTEM kommuniziert nicht direkt mit externen Behördensystemen
2. Das SYSTEM versendet keine automatischen Benachrichtigungen an betroffene Kunden

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess?
2. @Product Owner: Welche Rollen und Berechtigungen müssen abgebildet werden?
3. @Compliance Officer: Gibt es regulatorische Anforderungen an die Aufbewahrungsdauer der Protokolle?

### Warum dieses Beispiel funktioniert

- Die Erfolgskriterien sind **Outcome-orientiert**: "vollständig digital durchlaufen" (nicht "System kann Marktrückzüge verwalten"), "rekonstruierbar" (nicht "Änderungsprotokoll existiert"), "kein User kann" (nicht "Berechtigungen sind implementiert")
- Die Erfolgskriterien sind **selbst-verifizierend**: Jedes Kriterium ist so spezifisch, dass ein Stakeholder sofort weiss, was er prüfen müsste — ohne dass eine Verifikationsmethode vorgeschrieben wird
- **Keine Verifikationsmethode** im Kriterium — wie genau geprüft wird (Walkthrough, Testprotokoll, Demo) entsteht auf Story-Ebene

## Golden Example: Enabler Epic

MHP-Datenmodell für Medizin- und Hygieneprodukte

Als Entwicklungsteam
möchte ich zusammen mit dem Auftraggeber ein vollständiges Verständnis über die Medizin- und Hygieneproduktdaten von swissdamed erhalten
damit ich die Daten strukturiert in die Applikation übernehmen kann

Preconditions
1. Der Zugang zu swissdamed-Daten (XML-Export, Data Dictionary V2.0) ist gewährleistet
2. Die EMDN-Referenzdaten (Hierarchie, Vergleichscodes) liegen vor
3. Endbenutzer der Meldestelle sind für fachliche Klärungen erreichbar
4. Der Entscheid für einen eigenen Bounded Context (ies-mhp) ist getroffen

Erfolgskriterien
1. Für jedes swissdamed-Pflichtfeld ist dokumentiert, ob es ins MHP-Zieldatenformat übernommen, transformiert oder ignoriert wird, inklusive Begründung
2. Die Mengenkennzahl für Pflichtlager ist mit Einheit, Granularität und Berechnungsformel definiert und vom PO schriftlich abgenommen
3. Die Produktidentifikation ist als Entscheidungsdokument festgehalten mit Begründung, warum der gewählte Primärschlüssel gegenüber Alternativen bevorzugt wird
4. Für Hygieneprodukte ist eine Datenquelle mit Bewertung (Vollständigkeit, Integrierbarkeit, Lizenz) identifiziert, oder es liegt eine dokumentierte Analyse von mindestens 2 evaluierten Quellen mit Begründung der Ablehnung und empfohlenem nächsten Schritt vor
5. Für fehlende oder inkonsistente swissdamed-Daten ist pro betroffenem Feld eine Fallback-Regel mit Verantwortlichkeit und Eskalationsweg definiert
6. Die EMDN-Hierarchie ist mit Empfehlung der Aggregationsebene für MHP-Zwecke dokumentiert, inklusive Begründung warum EMDN allein für Austauschbarkeit nicht ausreicht
7. Der PO hat das konsolidierte Analysedokument mit allen Teilergebnissen schriftlich freigegeben

Out of Scope
1. Das MHP-Domänenmodell wird nur als Zieldatenformat dokumentiert, nicht als lauffähiger Code umgesetzt
2. Der EMDN-Code ist kein Pendant zum ATC-Code für Austauschbarkeit — zwei Produkte mit identischem EMDN-Code können klinisch nicht austauschbar sein
3. Die funktionale Spezifikation der Alternativensuche ist nicht Teil der Analyse, jedoch wird die Datenbasis dafür bewertet

Offene Fragen
1. @PO: Welche primäre Mengenkennzahl soll für ePL/Pflichtlager verwendet werden unter Berücksichtigung von MepV und ePL-Verordnung MP?
2. @Fachexperte Meldestelle: Welche swissdamed-Attribute werden in der Praxis tatsächlich für die Produktidentifikation genutzt?

### Warum dieses Beispiel funktioniert

- Es ist ein **Enabler Epic**: Das Ergebnis ist Wissen und Entscheide, kein nutzbares Feature — Output und Outcome fallen zusammen
- Die Erfolgskriterien sind **spezifisch im Qualitätsniveau**: nicht "ein Mapping liegt vor", sondern "für jedes Pflichtfeld ist dokumentiert ob übernommen, transformiert oder ignoriert, inklusive Begründung"
- Erfolgskriterium 4 zeigt den **Oder-Pfad**: Entweder eine Quelle gefunden oder dokumentiert warum nicht — beide Ergebnisse sind ein Erfolg
- Erfolgskriterium 7 ist das **Abnahme-Kriterium**: Der PO gibt das Gesamtdokument frei — das schliesst den Bogen zur Auftragnehmer-Abnahme
- Out of Scope enthält **keine Verweise auf Nachbar-Epics** ("wird in Epic X gemacht") — stattdessen nur Punkte, die ein Leser fälschlicherweise mit hineininterpretieren könnte: eine Implementierungs-Einschränkung (Punkt 1), eine fachliche Fehlvorstellung (Punkt 2), eine Abgrenzung gegenüber verwandter Funktionalität (Punkt 3)
