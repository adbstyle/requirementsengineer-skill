# Anti-Pattern-Katalog für Anforderungstexte

Gilt für Preconditions, Acceptance Criteria, Postconditions, Out of Scope und Erfolgskriterien. Zwei Leser:
- Der Requirements Engineer liest den Katalog in Phase 3, bevor er AKs und Postconditions schreibt.
- Der Regel-Prüfer (Phase 4, Agent 7) arbeitet die Checkliste Satz für Satz ab.

Den Rahmen bilden die drei Prüfungen aus SKILL.md: Notwendigkeit, Eine Regel ein Satz, Austauschbarkeit. Die einzelnen Anti-Patterns sind bekannte Formen, in denen eine dieser Prüfungen scheitert, dazu kommen einige Formregeln.

## Checkliste

**Form**
- Fett-Formatierung, Zwischenüberschriften oder Titel-Präfixe in den AKs
- GIVEN-WHEN-THEN oder Gherkin
- Halbsatz mit Gedankenstrich als Krücke
- Satz ohne Akteur oder im Passiv
- Verweis auf Tickets, Stories, offene Fragen (Q-Nummern) oder Dokumente, auch in Out of Scope

**Notwendigkeit:** Geht etwas verloren, wenn der Satz fehlt?
- Implizites Duplikat: dieselbe Aussage aus zwei Perspektiven
- Sonderfall-Implikat: Satz B folgt aus dem allgemeineren Satz A
- Precondition als Qualifier im AK wiederholt
- AK, dessen Ort aus einer Precondition und dessen Fähigkeit aus einem anderen AK folgt
- Schwächere Fähigkeit neben stärkerer: «kann einsehen» neben «darf ändern», «kann finden» neben «kann löschen», Constraint-AK «nur für berechtigte USER» neben «der berechtigte USER kann»
- Postcondition, die bestätigt, was ein AK, das Glossar oder die einführende Nachbar-Story schon regelt
- Selbstverständlichkeit oder universeller Qualitätsstandard als AK
- Explizit aufgezähltes Komplement nach «nur» oder «ausschliesslich»

**Eine Regel, ein Satz**
- Dieselbe Regel einmal positiv und einmal verneint
- Ausnahme oder Einschränkung als eigener Satz zu einer Regel, die in einem anderen Satz steht

**Austauschbarkeit:** Lässt der Satz mehrere plausible Lösungen zu?
- Ort der Anzeige: Detailseite, Startseite, Dialog, Liste, «in der Übersicht anzeigen»
- Weg: navigieren, gelangen, wechseln, «über X», «mittels Y», «via Z», «mit einem Klick»
- Zeitpunkt und Auslöser: «nach dem Login», «beim Öffnen», «landet auf», «wird weitergeleitet»
- Lösungsweg aus einer Vorgabe übernommen: Vertrag, Requirement-Abgrenzung, Codebase, Story-Satz der Vorlage
- Mechanik der Lösung, UI-Vergleichsreferenz, konkrete Wertelisten oder Enums, Klammer-Beispiele
- Implementierungsdetail oder interner Mechanismus (WIE statt WAS)

**Unabhängigkeit und Herkunft** (Details in SKILL.md)
- Fremde Fähigkeit in AK oder Postcondition (Einführungsprinzip)
- Precondition ohne Herkunft (Herkunftsregel)
- Out-of-Scope-Punkt, dessen einziger Inhalt ist, dass eine Nachbar-Story etwas liefert

**Kein Verstoss** (nicht melden)
- Die AK-Form «Der USER erkennt / kann / muss …». Sie ist vorgeschrieben.
- Das SYSTEM als Akteur in einem AK für eine Einschränkung, eine Validierung oder ein Recht, das die Story einführt (AK 1)
- AK «Der USER kann X löschen» neben Postcondition «Das SYSTEM löscht X WENN der USER bestätigt hat». Das eine ist eine Möglichkeit, das andere ein Ergebnis mit Bedingung.
- Fehlende UI-Details. Lösungsoffenheit ist gewollt.
- Eine Precondition, ohne die eine Aktion der AKs nicht ausführbar wäre, etwa weil der Akteur das Objekt sonst nicht finden oder abfragen kann. Sie ist nicht überflüssig, auch wenn sie selbstverständlich klingt.

## Beispiele zu den drei Prüfungen

**Notwendigkeit**

Statt (AK wiederholt Precondition und ein anderes AK):
  Precondition: Der USER zeigt einen Eintrag im Detail an
  AK 2: Der USER kann die vorbelegten Werte übernehmen oder ändern
  AK 5: Der USER kann die Werte in der Detailansicht des Eintrags anzeigen und ändern
Richtig: AK 5 streichen. Der Ort steht in der Precondition, das Ändern in AK 2.

Statt (schwächere Fähigkeit neben stärkerer):
  AK 3: Das SYSTEM lässt das Ändern der Werte für alle USER zu, mit deren Organisation der Eintrag geteilt ist
  AK 6: Der USER der prüfenden Organisation kann die Werte samt Typ einsehen
Richtig: AK 6 streichen. Der Eintrag ist immer mit der prüfenden Organisation geteilt, und wer ändern darf, sieht die Werte. Den eigenen Anteil «samt Typ» vorher in ein bestehendes AK verlagern, falls er gebraucht wird.

Statt (Postcondition bestätigt Geregeltes):
  PC: Das SYSTEM führt den erfassten Eintrag als eigenen Eintrag neben bestehenden Einträgen derselben Person
Richtig: streichen. Ein AK und das Glossar sagen bereits, dass mehrere Einträge pro Person möglich sind.

Grenze (tragende Precondition, die nicht gestrichen werden darf):
  Precondition: Der USER hat das Recht, die Einträge seiner und aller untergeordneten Organisationen anzuzeigen
  AK 1: Das SYSTEM stellt die Berechtigung zum Herunterladen von Einträgen zur Zuweisung bereit
  AK 2: Der berechtigte USER kann die Einträge seiner und aller untergeordneten Organisationen herunterladen
Falsch wäre, die Precondition zu streichen, weil Download-Recht und Organisationsgrenze jeden Zugriffsweg abdecken. Ohne Anzeigerecht weiss der USER nicht, welche Einträge es gibt, auch ein technischer User nicht. Die Precondition bleibt.

**Eine Regel, ein Satz**

Statt (positiv und verneint):
  AK 4: Der ADMIN kann den Eintrag für eine Person aus dem berechtigten Personenkreis erfassen
  AK 5: Der ADMIN kann keinen Eintrag für eine Person erfassen, die dem berechtigten Personenkreis nicht angehört
Richtig:
  AK 4: Der ADMIN kann den Eintrag nur für eine Person aus dem berechtigten Personenkreis erfassen

Statt (Ausnahme als eigener Satz):
  PC 1: Das SYSTEM versendet die Benachrichtigung an alle User, die sie abonniert haben, WENN ein USER einen Eintrag erstellt oder ändert
  PC 2: Das SYSTEM versendet die Benachrichtigung nicht an den USER, der den Eintrag erstellt oder geändert hat
Richtig:
  PC 1: Das SYSTEM versendet die Benachrichtigung an alle anderen User, die sie abonniert haben, WENN ein USER einen Eintrag erstellt oder ändert

**Austauschbarkeit**

Statt (Ort und Weg): Aus der Übersicht gelangen ADMINs zur Detailseite eines Eintrags
Statt (Ort als Rest): Der USER kann zu den Einträgen in der Übersicht Detailinformationen anzeigen
Richtig: Der USER kann von der Übersicht aus zu jedem angezeigten Eintrag Detailinformationen erreichen

Statt (Zeitpunkt und Einstieg): ADMINs und USER gelangen nach dem Login auf eine Startseite mit den Inhalten ihrer Rolle
Richtig: ADMINs und USER können ein Dashboard mit den Inhalten ihrer Rolle anzeigen

Statt (erlaubter Lösungsweg als Anforderung): Die angezeigte Ansicht lässt sich über den Druckdialog des Browsers drucken und als PDF speichern
Richtig: Die angezeigte Ansicht kann gedruckt oder als PDF gespeichert werden
Die Abgrenzung «keine Druckoptimierung über den Browser-Standard hinaus» gehört in Out of Scope.

## Weitere Regeln, Litmus-Tests und Beispiele

❌ KEINE Fett-Formatierung (**bold**) in Story-Texten — Klartext, keine Markdown-Deko
❌ KEINE Zwischenüberschriften oder Kategorie-Titel innerhalb der Acceptance Criteria — die AKs sind eine flache, durchnummerierte Liste ohne Gruppierung. Subtitels wie "Erstellen", "Anzeigen", "Bearbeiten", "Löschen" etc. zwischen den AKs sind unnötig und stören den Lesefluss. Die Nummerierung allein gibt Struktur genug.
❌ KEINE Titel-Präfixe vor AKs wie "**Create:** Das SYSTEM..." oder "**Delete:** Das SYSTEM..." — jedes AK beginnt direkt mit dem Akteur
❌ KEINE fremden Fähigkeiten in AKs oder Postconditions — AKs und Postconditions beschreiben ausschliesslich, was DIESE Story einführt. Setzt ein AK eine Fähigkeit voraus, die eine andere Story einführt, gehört das AK in jene Story (Einführungsprinzip). Abhängigkeiten selbst sind legitim — ihr Platz sind die Preconditions, als Zustand formuliert. Litmus: "Kann diese Story umgesetzt und abgenommen werden, sobald ihre Preconditions erfüllt sind — ohne dass eine andere Story gleichzeitig fertig werden muss?" → Nein = ein AK oder eine Postcondition trägt fremden Scope (siehe SKILL.md, Abschnitt "Story-Unabhängigkeit: Vertikaler Schnitt und Einführungsprinzip")
❌ KEINE Referenzen in AKs — weder auf andere Stories/Tickets ("Story 11", "IES-12345"), noch auf offene Fragen ("gem. Q20", "gem. Q-NEU-1"), noch auf externe Dokumente. Der Leser muss jedes AK verstehen, ohne etwas nachzuschlagen. Information inline wiederholen. Wenn ein Detail noch ungeklärt ist: AK so weit formulieren wie möglich und das offene Detail als Frage in die Offene-Fragen-Tabelle verschieben — NICHT als "gem. Q-xyz"-Platzhalter im AK parken.
❌ AVOID GIVEN-WHEN-THEN notation or Gherkin syntax
❌ KEINE Implementierungsdetails in AKs — AKs beschreiben WAS das System tut, nicht WIE es das intern löst. Typischer Fehler: Codebase-Analyse liefert technische Details, die ungefiltert in AKs landen.
❌ KEINE impliziten Duplikate — dasselbe Verhalten nicht einmal positiv und einmal negativ (oder aus System- und User-Perspektive) formulieren. Jedes AK muss einen eigenständigen, testbaren Wert liefern. Wenn ein AK logisch aus einem anderen folgt, ist es redundant.
❌ KEINE Wiederholung einer Precondition als Qualifier im AK — wenn ein AK seine Aktion durch einen Relativsatz oder Einschub einschränkt ("..., in dem/der er X ist", "..., sofern er X ist", "..., wenn er X hat"), der bereits als Precondition steht, ist der Zusatz redundant. Die Preconditions gelten für die ganze Story; ein AK muss sie nicht erneut qualifizieren. Litmus: Streiche den Nebensatz — bleibt die Aktion testbar UND steht die Bedingung schon in den Preconditions? Dann gehört der Nebensatz nicht ins AK. Steht die Bedingung NICHT oben, ist sie eine fehlende Precondition — dorthin verschieben, nicht ins AK packen.
❌ KEINE Halbsatz-Konstrukte mit Gedankenstrich (—) — ein AK ist ein vollständiger, einfacher Aussagesatz. Der Gedankenstrich wird oft als Krücke benutzt, um einen vagen ersten Teil mit einer Erklärung oder Einschränkung zu retten. Stattdessen: den Gedanken zu Ende denken und als eigenständigen Satz formulieren. Wenn ein AK zwei Aussagen enthält, in zwei AKs aufteilen.
❌ KEINE konkreten Wertelisten oder Enums in AKs — Aufzählungen wie "(PERSON, ORT, DATUM, KONTAKT, ORGANISATION, MEDIZINISCH, SONSTIGES)" oder "wählt aus A, B, C, D" sind Lösungsdaten. Das konkrete Set gehört ins Datenmodell der späteren Spec oder in eine Anmerkung — niemals auf Anforderungsebene. Das AK beschreibt die Fähigkeit, nicht den Inhalt der Auswahl.
❌ KEINE Klammer-Beispiele oder Klammer-Aufzählungen in AKs — Klammern wie "(z.B. X, Y, Z)", "(Aktion A, Aktion B, ...)" oder konkrete Display-Strings wie '("1 Eintrag" / "{n} Einträge")' sind Mechanik bzw. Beispiele aus der Spec. Sie überspezifizieren die Anforderung, sind fehleranfällig (vergessenes Element verfälscht die Aussage) und blähen den Satz auf. Streiche die Klammer und prüfe: Trägt der Satz davor allein? Wenn ja → fertig. Wenn nein → der Klammer-Inhalt war der eigentliche funktionale Kern; formuliere DAS als AK.
❌ KEINE Selbstverständlichkeiten/universellen Qualitätsstandards als AK — Aussagen wie "Text ist grammatikalisch korrekt" sind Standards, keine Story-AKs. Wenn dahinter ein funktionaler Kern steckt (z.B. dynamische Einzahl/Mehrzahl, Live-Validierung, Breakpoint-Logik), formuliere DEN als AK — nicht das Qualitätsmerkmal "verziert" mit Beispielen in Klammern als Beweis.
❌ KEIN explizit aufgezähltes Komplement — wenn ein AK "ausschliesslich X" oder "nur wenn X" sagt, ist alles andere logisch bereits ausgeschlossen. Das Komplement zusätzlich aufzulisten ("nicht Y, nicht Z, nicht W") liefert keinen Mehrwert und ist fehleranfällig: ein vergessenes Element verfälscht die Aussage. Vertraue auf die Logik von "ausschliesslich" / "nur".
❌ KEINE Sonderfall-Implikate — wenn AK B nur einen Spezialfall einer allgemeineren Regel in AK A formuliert, ist B redundant. Beispiel: A "Anzahl wird nur angezeigt wenn > 0" deckt B "keine Anzeige bei 0 Wörtern" zwingend ab (0 Wörter → 0 Treffer → durch A bereits ausgeschlossen). Der einfache Duplikat-Test ("können beide unterschiedliche Wahrheitswerte haben?") greift hier nicht — weil A und B unterschiedliche Bedingungen prüfen, B aber durch A garantiert wird. Schärferer Test siehe unten.
❌ KEINE Mechanik der Lösung im AK — Zusätze wie "der aktuelle Typ wird ausgeblendet", "ohne ein Menü zu öffnen", "als Supporting-Text", "mit einem Klick", "über einen Quick-Action-Button" beschreiben wie die Lösung sich verhält, nicht was der USER können muss. Litmus: Bleibt die Anforderung intakt, wenn alles nach dem ersten Komma oder Semikolon gestrichen wird? Wenn ja → den Zusatz streichen. Mechanik gehört in die Spec, nicht in die Anforderung.
❌ KEINE UI-Vergleichsreferenzen ("identisch zum Inline-Chip-Menü", "analog zum X", "wie im Y", "gleich wie in Z") — das sind Konsistenzregeln für Design/Spec, nicht für Anforderungen. Die Anforderung beschreibt, was der USER braucht, nicht woher er es kennt.

Litmus-Test gegen Lösungstext (für jedes AK durchziehen):
- "Würde ein PO diesen Satz auch ohne Designvorlage genau so schreiben?" → Nein = zu lösungsgetrieben, runterstrippen.
- "Bleibt der testbare Kern intakt, wenn ich alles nach dem Verb des USERs streiche?" → Ja = den Rest streichen.
- "Steht ein konkretes Set, eine UI-Bezeichnung in Anführungszeichen, ein Vergleich zu einem anderen Element drin?" → meist raus.
- "Steht eine Klammer im Satz?" → Klammer streichen und prüfen, ob der Satz davor allein trägt. Wenn ja → fertig. Wenn nein → der Klammerinhalt war der eigentliche Kern; den verbalisieren, nicht den Rahmen.
- "Ist das, was ich als AK schreibe, in jeder UI ohnehin Pflicht (grammatikalisch korrekt, barrierefrei, validiert, responsiv)?" → Ja = Selbstverständlichkeit, raus. Wenn ein Mechanismus dahinter steckt (dynamische Einzahl/Mehrzahl, Live-Validierung), DEN formulieren.
- "Zähle ich nach 'ausschliesslich' / 'nur' das Komplement explizit auf?" → Komplement-Aufzählung streichen; die Logik des Quantors trägt die Aussage.
- "Hängt ein Relativsatz/Einschub die Ausgangslage an ('..., in dem/der/sofern/wenn er X ist')?" → Prüfen ob X schon Precondition ist. Wenn ja → Nebensatz streichen. Wenn nein → X als Precondition ergänzen, AK trotzdem entschlacken.
- "Wer führt ein, was diese Precondition voraussetzt?" → Eine frühere Story: bleibt. Diese Story: streichen, die Fähigkeit bleibt im AK. Niemand: streichen — die Story liefert es dann selbst (Default), oder eine eigene Story ist nötig. Blosse Wortüberschneidung ist kein Treffer: Eine Precondition kann das Recht zum Anzeigen von Einträgen voraussetzen, während die Story die Berechtigung zum Herunterladen einführt (siehe das Beispiel «Grenze» weiter oben und die Herkunftsregel in SKILL.md).
- "Frage ich in den Offenen Fragen nach dem INHALT von etwas, das eine Precondition als vorhanden behauptet?" ("Welche Kategorien sollen hinterlegt werden?" neben "Kategorien sind im System hinterlegt") → Widerspruch. Wenn du fragst, welche es sein sollen, existieren sie nicht. Precondition streichen, die Frage bleibt.

Statt (Precondition als Qualifier im AK wiederholt):
  Precondition: Der USER ist als aufgenommene*r Freiwillige*r im Freiwilligenkreis des Angebots geführt
  AK: Der USER kann aus dem Freiwilligenkreis eines Angebots austreten, in dem er als aufgenommene*r Freiwillige*r geführt ist
Richtig (AK nur die Aktion, Bedingung bleibt in der Precondition):
  Der USER kann aus dem Freiwilligenkreis eines Angebots austreten

Statt (Lösung im AK):
  Der USER kann unter "Typ ändern" aus PERSON, ORT, DATUM, KONTAKT, ORGANISATION wählen; der aktuelle Typ wird ausgeblendet
Richtig (Anforderung pur):
  Der USER kann den Typ ändern

Statt (UI-Vergleich + Mechanik):
  Der USER sieht beim Eintrag "Pseudonym entfernen" den Originaltext und die Vorkommenshäufigkeit als Supporting-Text, identisch zum Inline-Chip-Menü
Richtig (Bedürfnis):
  Der USER erkennt den Originaltext und die Vorkommenshäufigkeit

Statt (Quick-Action-Mechanik):
  Der USER kann die Pseudonymisierung über einen Quick-Action-Button auf der Listen-Zeile mit einem Klick zurücknehmen, ohne ein Menü zu öffnen
Richtig:
  Der USER kann die Pseudonymisierung schnell und einfach rückgängig machen

Duplikat-Litmus-Test (zweistufig):
1. **Symmetrischer Test** — "Kann AK A wahr sein, während AK B falsch ist (und umgekehrt)?" → Nein in beide Richtungen = identische Aussage, eines streichen.
2. **Implikations-Test** — "Wenn AK A gilt, ist dann AK B automatisch erfüllt, ohne dass B etwas Eigenständiges hinzufügt?" → Ja = B ist Sonderfall/Implikat von A, B streichen.

Der Implikations-Test fängt den Fall, in dem zwei AKs unterschiedliche Bedingungen prüfen, B aber durch A garantiert wird (z.B. A "nur wenn > 0" deckt B "0 Wörter → nicht angezeigt" zwingend ab — 0 Wörter erzwingt 0 Treffer, das ist bereits durch A geregelt). Solche AKs liefern keinen testbaren Mehrwert.

Statt (Selbstverständlichkeit + Klammer-Beispiel als Beweis):
  Der USER sieht die Anzahl in grammatikalisch korrektem Deutsch ("1 Pseudonymisierung" im Singular, "{n} Pseudonymisierungen" ab 2)
Richtig (funktionaler Kern):
  Der USER sieht die Anzahl mit dynamischer Einzahl/Mehrzahl-Unterscheidung

Statt (Klammer-Aufzählung als Beispielcontainer + überflüssige "nachdem"-Erklärung):
  Der USER sieht eine aktualisierte Anzahl, nachdem sich der Inhalt der Session im Review-Editor durch eine seiner Aktionen verändert hat (Chip-Entfernung, Quick-Add zur Sperrliste, Batch-Revert, Typ-Wechsel, Undo)
Richtig (Kern):
  Der USER sieht jederzeit die aktuelle Anzahl zum Inhalt der Session

Statt (explizit aufgezähltes Komplement nach "ausschliesslich"):
  Der USER sieht die Anzahl ausschliesslich bei Sessions im Status "review", nicht bei Sessions in den Status "recording", "queued", "processing" oder "error"
Richtig (Komplement implizit):
  Der USER sieht die Anzahl ausschliesslich bei Sessions im Status "review"

Statt (Sonderfall-Implikat — durch allgemeineres AK bereits abgedeckt):
  AK 4. Der USER sieht die Anzahl nur, wenn sie grösser als 0 ist
  AK 8. Der USER sieht keine Pseudonymisierungs-Anzahl, wenn die Session 0 Wörter hat
Richtig (allgemeineres AK behalten, Sonderfall streichen):
  AK 4. Der USER sieht die Anzahl nur, wenn sie grösser als 0 ist

Statt (Zwischenüberschriften in AKs — unnötige Gruppierung):
  Erstellen
  1. Der USER kann eine Word-Datei hochladen.
  2. Der USER muss beim Hochladen einen Titel angeben.
  Anzeigen
  3. Der USER kann alle Vorlagen einsehen.
  Löschen
  4. Der USER kann eine Vorlage löschen.
Richtig (flache, durchnummerierte Liste):
  1. Der USER kann eine Word-Datei hochladen.
  2. Der USER muss beim Hochladen einen Titel angeben.
  3. Der USER kann alle Vorlagen anzeigen.
  4. Der USER kann eine Vorlage löschen.

Statt (implizites Duplikat — gleiche Aussage, verschiedene Perspektiven):
  2. Das SYSTEM verarbeitet den Import im Hintergrund — der USER wartet nicht auf den Abschluss
  3. Der USER kann während der Verarbeitung in der Applikation weiterarbeiten
Richtig (eine Aussage, die den testbaren Kern trifft):
  2. Der USER kann während der Verarbeitung in der Applikation weiterarbeiten

WAS-vs-WIE Litmus-Test für jedes AK:
- "Muss der User/PO das wissen, um die Anforderung zu verstehen?" → Ja = WAS, Nein = WIE
- "Schränkt das die Entwickler unnötig ein?" → Ja = WIE, raus aus AK
- "Beobachtbares Verhalten oder interner Mechanismus?" → Mechanismus = WIE

Statt (WIE — Erkennungsmechanismus):
  3. Das SYSTEM erkennt die Aktion: leere id-Spalte = Create, existierende id = Update, delete-Spalte = true = Delete
Richtig (WAS — beobachtbares Verhalten):
  3. Das SYSTEM unterscheidet pro Zeile, ob eine Einrichtung erstellt, aktualisiert oder gelöscht werden soll

Statt (WIE — interne Verarbeitungslogik):
  4. Das SYSTEM verarbeitet in der Reihenfolge: zuerst Create, dann Update, dann Delete
Richtig (WAS — beobachtbares Ergebnis, nur falls fachlich relevant):
  4. Das SYSTEM stellt sicher, dass neu erstellte Einrichtungen im selben Import aktualisiert oder gelöscht werden können

Statt (WIE — Technologie und Architektur):
  PC1. Erstellte Einrichtungen sind über MessageHub an Downstream-Services (ies-koordination/einsatz) propagiert
Richtig (WAS — beobachtbarer Zustand):
  PC1. Erstellte Einrichtungen sind in der Organisation sichtbar

Statt (Formatierung & Referenzen):
  4. **Create:** Das SYSTEM erstellt eine neue Einrichtung (Feld-Tabelle aus Story 11)
  7. **Delete:** Das SYSTEM ruft die bestehende Löschlogik auf
Richtig:
  4. Das SYSTEM erstellt eine neue Einrichtung unter der angegebenen parent_organisation_id mit den Feldern Name, GeoPosition, Spitalkategorie, Phonenumber, Versorgung
  7. Das SYSTEM löscht eine Einrichtung NUR WENN keine Leistungen zugeordnet sind

Statt (Q-Referenz als Platzhalter — Detail ungeklärt ins AK geschoben):
  2. Das SYSTEM erkennt die Aktion pro Zeile — ausser eine explizite Delete-Spalte ist gesetzt (Spaltenname/Format gem. Q-NEU-2)
  3. Das SYSTEM identifiziert Organisationen anhand des Lookup-Keys (Lookup-Key gem. Q20)
Richtig (so weit formulieren wie bekannt, Unklares in Offene Fragen):
  2. Das SYSTEM erkennt die gewünschte Aktion pro Zeile: leerer Lookup-Key bedeutet Create, vorhandener Lookup-Key bedeutet Update, gesetzte Delete-Spalte bedeutet Deaktivierung
  3. Das SYSTEM identifiziert bestehende Organisationen anhand eines eindeutigen Schlüsselfelds im CSV
  → Falls unklar welches Feld/welches Format: Offene Frage anlegen, NICHT "gem. Q-xyz" ins AK schreiben

Statt (Ticket-Referenz in AK):
  7. Der Import-Vorgang ist in der Import-Übersicht nachvollziehbar (IES-17623)
Richtig (Anforderung selbsterklärend formulieren):
  7. Der Import-Vorgang ist in der Import-Übersicht nachvollziehbar
