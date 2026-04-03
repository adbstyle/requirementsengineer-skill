# Golden Example: Vollständig ausgefüllte User Story

Dieses Beispiel zeigt den erwarteten Stil und die Form einer fertigen User Story. Nutze es als Referenz fuer Satzstruktur, Detailgrad und Formatierung.

## Stilregeln (zusammengefasst am Beispiel ablesbar)

- Jedes AK ist ein vollstaendiger, einfacher Aussagesatz
- Ein Gedanke pro Satz, kein Gedankenstrich (—) als Kruecke
- Kein Bold, keine Zwischenueberschriften, keine Referenzen in AKs
- Akteur steht am Satzanfang: "Der USER..." oder "Das SYSTEM..."
- Preconditions beschreiben Zustaende VOR der Interaktion
- Postconditions beschreiben Ergebnisse NACH Abschluss der Interaktion
- Offene Fragen enthalten nur unbeantwortete Fragen an andere Stakeholder

---

## Beispiel 1: Standardfall (CRUD mit Geschaeftsregeln)

Dokumentvorlage verwalten

Als Sachbearbeiter
moechte ich Word-Vorlagen fuer Bescheide hochladen, einsehen und entfernen koennen
damit ich die Korrespondenz mit aktuellen Dokumentvorlagen fuehren kann

Preconditions
1. Der USER ist an der Applikation angemeldet
2. Der USER besitzt die Rolle Vorlagenverwaltung

Acceptance Criteria
1. Der USER kann eine Word-Datei im Format .docx hochladen
2. Der USER muss beim Hochladen einen eindeutigen Titel fuer die Vorlage angeben
3. Das SYSTEM lehnt den Upload ab, wenn der Titel bereits vergeben ist
4. Das SYSTEM lehnt Dateien ab, die groesser als 10 MB sind
5. Das SYSTEM zeigt eine Fehlermeldung mit dem konkreten Grund an, wenn der Upload abgelehnt wird
6. Der USER kann alle verfuegbaren Vorlagen in einer Liste einsehen
7. Die Liste zeigt pro Vorlage den Titel, das Hochladedatum und den Namen des Erstellers an
8. Der USER kann eine Vorlage aus der Liste loeschen
9. Das SYSTEM fragt vor dem Loeschen eine explizite Bestaetigung ab

Postconditions
1. Eine hochgeladene Vorlage steht allen Sachbearbeitern mit der Rolle Vorlagenverwaltung zur Verfuegung
2. Eine geloeschte Vorlage ist nicht mehr in der Liste sichtbar und kann nicht mehr fuer neue Bescheide verwendet werden
3. Bereits erstellte Bescheide, die auf einer geloeschten Vorlage basieren, bleiben unveraendert

Out of Scope
1. Versionierung von Vorlagen (eine neue Version wird als separate Vorlage hochgeladen)
2. Vorschau des Vorlageninhalts in der Applikation
3. Bearbeitung des Vorlageninhalts innerhalb der Applikation

Offene Fragen
1. @Fachexperte: Welche Platzhalter muss eine gueltige Vorlage enthalten, damit das System sie beim Bescheid-Erstellen befuellen kann?
2. @Product Owner: Soll die maximale Dateigroesse konfigurierbar sein oder reicht ein fester Wert?

---

## Beispiel 2: Berechtigungssteuerung (rollenbasiert)

Marktrückzug-Status verwalten

Als Regulatory-Affairs-Manager
moechte ich den Status eines Marktrückzugs entlang definierter Schritte aendern koennen
damit der Rückzugsprozess nachvollziehbar und kontrolliert ablaeuft

Preconditions
1. Der USER ist an der Applikation angemeldet
2. Ein Marktrückzug existiert im System

Acceptance Criteria
1. Der USER kann den Status eines Marktrückzugs auf den naechsten Schritt im Prozess setzen
2. Das SYSTEM erlaubt den Übergang von Entwurf auf Eingereicht nur fuer Rollen mit der Berechtigung Marktrückzug einreichen
3. Das SYSTEM erlaubt den Übergang von Eingereicht auf Freigegeben nur fuer Rollen mit der Berechtigung Marktrückzug freigeben
4. Das SYSTEM verhindert Statusübergaenge, die nicht im definierten Prozessablauf vorgesehen sind
5. Das SYSTEM protokolliert jeden Statusübergang mit Zeitpunkt, ausfuehrendem User und vorherigem Status
6. Nur Rollen mit Leseberechtigung auf das Entscheidfeld koennen dieses einsehen
7. Nur Rollen mit Schreibberechtigung auf das Entscheidfeld koennen dieses bearbeiten
8. Der USER sieht nur die Statusübergaenge als Aktionen, fuer die er berechtigt ist

Postconditions
1. Der Marktrückzug befindet sich im neuen Status
2. Der Statusübergang ist im Aenderungsprotokoll sichtbar

Out of Scope
1. Konfiguration der Prozessschritte durch den User (die Schritte sind fest definiert)
2. Automatische Benachrichtigungen bei Statusaenderungen

Offene Fragen
1. @Regulatory Affairs Lead: Welche konkreten Statusschritte umfasst der Marktrückzugsprozess (vollstaendige Liste)?
2. @Product Owner: Welche Rollen existieren und welche Berechtigungen hat jede Rolle auf welche Statusübergaenge?
3. @Fachexperte: Kann ein Statusübergang rückgaengig gemacht werden oder ist der Prozess nur vorwaerts gerichtet?
