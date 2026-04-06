# Golden Example: Vollständig ausgefüllte User Story

Dieses Beispiel zeigt den erwarteten Stil und die Form einer fertigen User Story. Nutze es als Referenz für Satzstruktur, Detailgrad und Formatierung.

## Stilregeln (zusammengefasst am Beispiel ablesbar)

- Jedes AK ist ein vollständiger, einfacher Aussagesatz
- Ein Gedanke pro Satz, kein Gedankenstrich (—) als Krücke
- Kein Bold, keine Zwischenüberschriften, keine Referenzen in AKs
- Akteur steht am Satzanfang: "Der USER..." oder "Das SYSTEM..."
- Preconditions beschreiben Zustände VOR der Interaktion
- Postconditions beschreiben Ergebnisse NACH Abschluss der Interaktion
- Offene Fragen enthalten nur unbeantwortete Fragen an andere Stakeholder

---

## Beispiel 1: Standardfall (CRUD mit Geschäftsregeln)

Dokumentvorlage verwalten

Als Sachbearbeiter
möchte ich Word-Vorlagen für Bescheide hochladen, einsehen und entfernen können
damit ich die Korrespondenz mit aktuellen Dokumentvorlagen führen kann

Preconditions
1. Der USER ist an der Applikation angemeldet
2. Der USER besitzt die Rolle Vorlagenverwaltung

Acceptance Criteria
1. Der USER kann eine Word-Datei im Format .docx hochladen
2. Der USER muss beim Hochladen einen eindeutigen Titel für die Vorlage angeben
3. Das SYSTEM lehnt den Upload ab, wenn der Titel bereits vergeben ist
4. Das SYSTEM lehnt Dateien ab, die grösser als 10 MB sind
5. Das SYSTEM zeigt eine Fehlermeldung mit dem konkreten Grund an, wenn der Upload abgelehnt wird
6. Der USER kann alle verfügbaren Vorlagen in einer Liste einsehen
7. Die Liste zeigt pro Vorlage den Titel, das Hochladedatum und den Namen des Erstellers an
8. Der USER kann eine Vorlage aus der Liste löschen
9. Das SYSTEM fragt vor dem Löschen eine explizite Bestätigung ab

Postconditions
1. Eine hochgeladene Vorlage steht allen Sachbearbeitern mit der Rolle Vorlagenverwaltung zur Verfügung
2. Eine gelöschte Vorlage ist nicht mehr in der Liste sichtbar und kann nicht mehr für neue Bescheide verwendet werden
3. Bereits erstellte Bescheide, die auf einer gelöschten Vorlage basieren, bleiben unverändert

Out of Scope
1. Das SYSTEM unterstützt keine Versionierung von Vorlagen — eine neue Version wird als separate Vorlage hochgeladen
2. Der USER kann den Inhalt einer Vorlage nicht in der Applikation ansehen
3. Der USER kann den Inhalt einer Vorlage nicht in der Applikation bearbeiten

Offene Fragen
1. @Fachexperte: Welche Platzhalter muss eine gültige Vorlage enthalten, damit das System sie beim Bescheid-Erstellen befüllen kann?
2. @Product Owner: Soll die maximale Dateigrösse konfigurierbar sein oder reicht ein fester Wert?

---

## Beispiel 2: Berechtigungssteuerung (rollenbasiert)

Marktrückzug-Status verwalten

Als Regulatory-Affairs-Manager
möchte ich den Status eines Marktrückzugs entlang definierter Schritte ändern können
damit der Rückzugsprozess nachvollziehbar und kontrolliert abläuft

Preconditions
1. Der USER ist an der Applikation angemeldet
2. Ein Marktrückzug existiert im System

Acceptance Criteria
1. Der USER kann den Status eines Marktrückzugs auf den nächsten Schritt im Prozess setzen
2. Das SYSTEM erlaubt den Übergang von Entwurf auf Eingereicht nur für Rollen mit der Berechtigung Marktrückzug einreichen
3. Das SYSTEM erlaubt den Übergang von Eingereicht auf Freigegeben nur für Rollen mit der Berechtigung Marktrückzug freigeben
4. Das SYSTEM verhindert Statusübergänge, die nicht im definierten Prozessablauf vorgesehen sind
5. Das SYSTEM protokolliert jeden Statusübergang mit Zeitpunkt, ausführendem User und vorherigem Status
6. Nur Rollen mit Leseberechtigung auf das Entscheidfeld können dieses einsehen
7. Nur Rollen mit Schreibberechtigung auf das Entscheidfeld können dieses bearbeiten
8. Der USER sieht nur die Statusübergänge als Aktionen, für die er berechtigt ist

Postconditions
1. Der Marktrückzug befindet sich im neuen Status
2. Der Statusübergang ist im Änderungsprotokoll sichtbar

Out of Scope
1. Der USER kann die Prozessschritte nicht selbst konfigurieren — die Schritte sind fest definiert
2. Das SYSTEM versendet keine automatischen Benachrichtigungen bei Statusänderungen

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess (vollständige Liste)?
2. @Product Owner: Welche Rollen existieren und welche Berechtigungen hat jede Rolle auf welche Statusübergänge?
3. @Fachexperte: Kann ein Statusübergang rückgängig gemacht werden oder ist der Prozess nur vorwärts gerichtet?
