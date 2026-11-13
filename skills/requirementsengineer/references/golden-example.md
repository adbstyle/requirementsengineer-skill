# Golden Example: Vollständig ausgefüllte User Story

Dieses Beispiel zeigt den erwarteten Stil und die Form einer fertigen User Story. Nutze es als Referenz für Satzstruktur, Detailgrad und Formatierung.

## Stilregeln (zusammengefasst am Beispiel ablesbar)

- Jedes AK ist ein vollständiger, einfacher Aussagesatz
- Ein Gedanke pro Satz, kein Gedankenstrich (—) als Krücke
- Kein Bold, keine Zwischenüberschriften, keine Referenzen in AKs
- **User Stories (Business):** AKs aus User-Sicht: Der USER ist der aktive Akteur ("Der USER kann...", "Der USER muss..."). Das SYSTEM in AKs nur bei Einschränkungen/Validierungen, die der User nicht steuert, und für ein Recht, das die Story einführt.
- **Enabler Stories:** AKs mit TEAM oder SYSTEM als Akteur ("Das TEAM hat...", "Das SYSTEM validiert..."). Kein USER als Akteur, weil der Endnutzer nicht direkt betroffen ist.
- Preconditions: nur nicht-offensichtliche Voraussetzungen ("User ist angemeldet" ist implizit). Nie etwas, das die Story selbst einführt: In Beispiel 1 wird die Rollenverwaltung vorausgesetzt (Precondition), die Berechtigung zur Vorlagenverwaltung dagegen eingeführt. Ihre Bereitstellung ist AK 1, weil alle weiteren AKs sie voraussetzen. Die folgenden AKs sprechen vom «berechtigten USER», ein zusätzliches Constraint-AK «nur für USER mit Berechtigung» entfällt.
- Eine Regel, ein Satz: Die Grenze einer Regel steht im selben AK («nur … bis 10 MB»), nicht in einem zweiten, verneinten AK
- Lösungsoffen: kein Ort und kein Weg («in einer Liste», «aus der Liste»), nur was der USER können muss
- Postconditions: System-Ergebnisse mit WENN-Bedingungen, keine Wiederholung der AKs
- Offene Fragen enthalten nur unbeantwortete Fragen an andere Stakeholder

---

## Beispiel 1: Standardfall (CRUD mit Geschäftsregeln)

Dokumentvorlage verwalten

Als Sachbearbeiter
möchte ich Word-Vorlagen für Bescheide hochladen, einsehen und entfernen können
damit ich die Korrespondenz mit aktuellen Dokumentvorlagen führen kann

Preconditions
1. Das SYSTEM verfügt über eine Rollenverwaltung, in der Berechtigungen Rollen zugewiesen werden

Acceptance Criteria
1. Das SYSTEM stellt die Berechtigung zur Verwaltung von Dokumentvorlagen zur Zuweisung bereit
2. Der berechtigte USER kann nur Word-Dateien im Format .docx bis 10 MB als Vorlage hochladen
3. Der berechtigte USER muss beim Hochladen einen Titel angeben, den keine andere Vorlage trägt
4. Der berechtigte USER kann alle verfügbaren Vorlagen anzeigen
5. Der berechtigte USER kann eine Vorlage löschen
6. Der berechtigte USER muss das Löschen einer Vorlage explizit bestätigen

Postconditions
1. Das SYSTEM stellt eine hochgeladene Vorlage allen berechtigten USERn zur Verfügung
2. Das SYSTEM entfernt die Vorlage endgültig WENN der USER das Löschen bestätigt hat
3. Das SYSTEM verändert keine bereits erstellten Bescheide, die auf einer gelöschten Vorlage basieren

Out of Scope
1. Das SYSTEM versioniert Vorlagen nicht
2. Der USER kann den Inhalt einer Vorlage nicht in der Applikation ansehen
3. Der USER kann den Inhalt einer Vorlage nicht in der Applikation bearbeiten

Offene Fragen
1. @Fachexperte: Welche Platzhalter muss eine gültige Vorlage enthalten, damit das System sie beim Bescheid-Erstellen befüllen kann?
2. @Product Owner: Soll die maximale Dateigrösse konfigurierbar sein oder reicht ein fester Wert?

---

## Beispiel 2: Enabler Story (Exploration/Architektur)

swissdamed-Importschnittstelle spezifizieren

Als Entwicklungsteam
möchte ich die Importschnittstelle für swissdamed-Daten technisch spezifizieren
damit die Implementierung des Datenimports auf einer abgestimmten Schnittstellendefinition aufbauen kann

Preconditions
1. Das MHP-Zieldatenformat ist als Analysedokument freigegeben
2. Der XML-Export von swissdamed ist als Testdatensatz verfügbar

Acceptance Criteria
1. Das TEAM hat für jedes Pflichtfeld im swissdamed-XML die Transformationsregel ins MHP-Zieldatenformat dokumentiert
2. Das TEAM hat die Fehlerbehandlung pro Feld spezifiziert (Fallback-Wert, Abbruch oder Warnung)
3. Das SYSTEM validiert einen Testdatensatz gegen das spezifizierte Schema ohne Fehler
4. Das TEAM hat die Importfrequenz und den Trigger-Mechanismus mit dem PO abgestimmt

Postconditions
1. Das SYSTEM enthält eine Schnittstellenspezifikation, die als Grundlage für die Implementierung des Datenimports dient
2. Das TEAM hat offene Transformationsfragen dokumentiert, die erst bei der Implementierung klärbar sind

Out of Scope
1. Das TEAM implementiert den Datenimport nicht
2. Das SYSTEM führt keine produktiven Datenimporte durch

Offene Fragen
1. @PO: Soll der Import vollautomatisch laufen oder manuell angestossen werden?

---

## Beispiel 3: Berechtigungssteuerung (rollenbasiert)

Marktrückzug-Status verwalten

Als Regulatory-Affairs-Manager
möchte ich den Status eines Marktrückzugs entlang definierter Schritte ändern können
damit der Rückzugsprozess nachvollziehbar und kontrolliert abläuft

Preconditions
1. Ein Marktrückzug existiert im System

Acceptance Criteria
1. Der USER kann den Status eines Marktrückzugs nur auf einen Schritt setzen, den der definierte Prozessablauf als nächsten vorsieht
2. Der USER kann nur Statusübergänge auslösen, für die seine Rolle berechtigt ist
3. Der USER kann das Entscheidfeld nur einsehen, wenn seine Rolle die Leseberechtigung dafür hat
4. Der USER kann das Entscheidfeld nur bearbeiten, wenn seine Rolle die Schreibberechtigung dafür hat

Postconditions
1. Das SYSTEM setzt den Marktrückzug auf den neuen Status WENN der USER den Übergang auslöst
2. Das SYSTEM protokolliert jeden Statusübergang mit Zeitpunkt, ausführendem User und vorherigem Status

Out of Scope
1. Der USER kann die Prozessschritte nicht selbst konfigurieren
2. Das SYSTEM versendet keine automatischen Benachrichtigungen bei Statusänderungen

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess (vollständige Liste)?
2. @Product Owner: Welche Rollen existieren und welche Berechtigungen hat jede Rolle auf welche Statusübergänge?
3. @Fachexperte: Kann ein Statusübergang rückgängig gemacht werden oder ist der Prozess nur vorwärts gerichtet?
