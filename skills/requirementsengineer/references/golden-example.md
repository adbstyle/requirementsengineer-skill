# Golden Example: Vollständig ausgefüllte User Story

Dieses Beispiel zeigt den erwarteten Stil und die Form einer fertigen User Story. Nutze es als Referenz für Satzstruktur, Detailgrad und Formatierung.

## Stilregeln (zusammengefasst am Beispiel ablesbar)

- Jedes AK ist ein vollständiger, einfacher Aussagesatz
- Ein Gedanke pro Satz, kein Gedankenstrich (—) als Krücke
- Kein Bold, keine Zwischenüberschriften, keine Referenzen in AKs
- **User Stories (Business):** AKs aus User-Sicht: Der USER ist der aktive Akteur ("Der USER kann...", "Der USER muss..."). Das SYSTEM in AKs nur bei Einschränkungen/Validierungen, die der User nicht steuert.
- **Enabler Stories:** AKs mit TEAM oder SYSTEM als Akteur ("Das TEAM hat...", "Das SYSTEM validiert..."). Kein USER als Akteur, weil der Endnutzer nicht direkt betroffen ist.
- Preconditions: nur nicht-offensichtliche Voraussetzungen ("User ist angemeldet" ist implizit)
- Postconditions: System-Ergebnisse mit WENN-Bedingungen, keine Wiederholung der AKs
- Offene Fragen enthalten nur unbeantwortete Fragen an andere Stakeholder

---

## Beispiel 1: Standardfall (CRUD mit Geschäftsregeln)

Dokumentvorlage verwalten

Als Sachbearbeiter
möchte ich Word-Vorlagen für Bescheide hochladen, einsehen und entfernen können
damit ich die Korrespondenz mit aktuellen Dokumentvorlagen führen kann

Preconditions
1. Der USER besitzt die Rolle Vorlagenverwaltung

Acceptance Criteria
1. Der USER kann eine Word-Datei im Format .docx hochladen
2. Der USER muss beim Hochladen einen eindeutigen Titel für die Vorlage angeben
3. Der USER kann alle verfügbaren Vorlagen in einer Liste einsehen
4. Der USER kann eine Vorlage aus der Liste löschen
5. Der USER muss das Löschen einer Vorlage explizit bestätigen
6. Das SYSTEM lehnt den Upload ab, wenn der Titel bereits vergeben ist oder die Datei grösser als 10 MB ist

Postconditions
1. Das SYSTEM speichert eine hochgeladene Vorlage und stellt sie allen Sachbearbeitern mit der Rolle Vorlagenverwaltung zur Verfügung
2. Das SYSTEM entfernt die Vorlage endgültig WENN der USER das Löschen bestätigt hat
3. Das SYSTEM verändert keine bereits erstellten Bescheide, die auf einer gelöschten Vorlage basieren

Out of Scope
1. Das SYSTEM unterstützt keine Versionierung von Vorlagen — eine neue Version wird als separate Vorlage hochgeladen
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
1. Das MHP-Zieldatenformat ist als Analysedokument freigegeben (Enabler Epic abgeschlossen)
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
1. Das TEAM implementiert den Datenimport nicht — nur die Spezifikation wird erstellt
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
1. Der USER kann den Status eines Marktrückzugs auf den nächsten Schritt im Prozess setzen
2. Der USER sieht nur die Statusübergänge als Aktionen, für die er berechtigt ist
3. Der USER kann das Entscheidfeld nur einsehen, wenn seine Rolle die Leseberechtigung dafür hat
4. Der USER kann das Entscheidfeld nur bearbeiten, wenn seine Rolle die Schreibberechtigung dafür hat
5. Das SYSTEM verhindert Statusübergänge, die nicht im definierten Prozessablauf vorgesehen sind

Postconditions
1. Das SYSTEM setzt den Marktrückzug auf den neuen Status WENN der USER den Übergang auslöst UND seine Rolle die Berechtigung für diesen Übergang hat
2. Das SYSTEM protokolliert jeden Statusübergang mit Zeitpunkt, ausführendem User und vorherigem Status

Out of Scope
1. Der USER kann die Prozessschritte nicht selbst konfigurieren — die Schritte sind fest definiert
2. Das SYSTEM versendet keine automatischen Benachrichtigungen bei Statusänderungen

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess (vollständige Liste)?
2. @Product Owner: Welche Rollen existieren und welche Berechtigungen hat jede Rolle auf welche Statusübergänge?
3. @Fachexperte: Kann ein Statusübergang rückgängig gemacht werden oder ist der Prozess nur vorwärts gerichtet?
