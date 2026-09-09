# Rückschreiben in den Tracker: chirurgische Änderungen (Phase 5)

Das Änderungsprotokoll des Trackers ist ein Arbeitsmittel: PO, Entwickler und Tester öffnen es,
um in Sekunden zu sehen, was sich seit ihrem letzten Blick geändert hat. Ersetzt du das
Beschreibungsfeld durch deine eigene Fassung, erscheint dort jede Zeile als geändert — auch die
achtzig, die identisch geblieben sind. Der Leser muss dann den ganzen Text erneut lesen und
selbst vergleichen, statt drei Zeilen zu prüfen. Genau diese Arbeit soll die Revisionshistorie
ihm abnehmen.

Deshalb gilt: **Das geschriebene Feld unterscheidet sich vom Bestand genau an den Stellen, an
denen sich der Inhalt geändert hat — und sonst nirgends.**

Die meisten Tracker-APIs können nur das ganze Feld ersetzen (Jira `description`, GitHub `body`,
Linear `description`). Der kleine Diff entsteht also nicht durch ein Teil-Update-API, sondern
dadurch, dass der unveränderte Rest zeichengleich mitgeschrieben wird. Der Bestand ist dein
Ausgangstext, nicht dein Chat-Output.

## Ablauf

1. **Bestand frisch holen.** Rufe das Feld unmittelbar vor dem Schreiben ab, im gleichen Format,
   das das Schreiben erwartet. Nicht die Agenten-Zusammenfassung aus Phase 2 verwenden — die ist
   gekürzt und normalisiert, und was du daraus rekonstruierst, ist nie zeichengleich.
2. **`before` ablegen.** Bestand unverändert in eine Datei im Scratchpad schreiben.
3. **`after` als Kopie von `before` erzeugen** und darin nur die inhaltlich geänderten Stellen
   ersetzen. Reihenfolge ist wichtig: kopieren, dann punktuell ändern — nicht neu schreiben und
   hoffen, dass es passt.
4. **Diff prüfen, bevor du schreibst** (`diff -u before after`). Enthält er eine Zeile, deren
   Inhalt gleich geblieben ist, ist der Schritt 3 misslungen → korrigieren, nicht schreiben.
   Ohne Shell-Zugang: `before` und `after` Zeile für Zeile gegenlesen und dasselbe prüfen.
5. **Schreiben** mit dem Ganzfeld-Update des Trackers.
6. **Nachkontrolle.** Feld erneut abrufen und gegen `after` vergleichen. Weicht es ab, hat der
   Tracker beim Round-Trip umformatiert (siehe Format-Fallen). Melde das dem User statt es
   stillschweigend hinzunehmen — er sieht den Grossdiff sonst erst im Protokoll.

## Kosmetik-Sperre: was unangetastet bleibt

Beim Lesen eines Bestandstextes entsteht fast zwangsläufig der Wunsch, ihn besser zu machen.
Jede dieser Verbesserungen kostet den Leser des Protokolls mehr, als sie ihm bringt.

**Formatierung.** Bullet-Zeichen (`-` vs. `*` vs. Nummern), Heading-Level, Bold/Kursiv,
Tabelle vs. Liste, Einrückung, Leerzeilen. Auch wenn das Golden Example flache nummerierte
Listen vorsieht und der Bestand Striche verwendet: Solange die Sektion inhaltlich unverändert
bleibt, bleibt sie unangetastet.

**Reihenfolge.** Sektionen und Listenpunkte bleiben, wo sie sind. Umsortieren erzeugt einen
Diff über den halben Text und ändert nichts an der Aussage.

**Wortwahl in unveränderten Passagen.** Keine Stilpolitur, keine Rechtschreibkorrektur, kein
Vereinheitlichen von "User"/"Nutzer"/"Anwender". Ein Tippfehler in einem AK, das du nicht
geändert hast, ist kein Teil deines Auftrags — nenne ihn dem User, wenn er dir auffällt, und
lass ihn im Text stehen. Auch die Akteursform aus dem Golden Example ("Der USER kann …") wird
nicht nachträglich über bestehende AKs gelegt: Sie gilt für AKs, die du schreibst, nicht für
solche, die schon dastehen. Ein Bestands-AK, das inhaltlich stimmt, ist kein Fehler, nur weil
es anders klingt als deines.

Umgekehrt gilt dasselbe für die Zeilen, die du **neu** einfügst: Sie übernehmen die Diktion des
Feldes, in das sie eingefügt werden. Ein neues "Der USER kann …" zwischen fünf bestehenden
"Der Nutzer kann …" ist kein sauberer Diff, sondern eine sichtbare Naht — und der erste Anlass
für den nächsten Leser, den Rest "anzugleichen". Willst du die Diktion umstellen, ist das ein
eigener Auftrag, den du dem User vorschlägst, statt ihn Zeile für Zeile einzuschmuggeln.

**Fremde Sektionen.** Dev Notes, Testhinweise, Anhänge, Schätzungen, Diskussionsnotizen: nicht
anfassen und erst recht nicht löschen, nur weil das Golden Example sie nicht vorsieht. Sie
gehören jemand anderem.

**Umnummerieren "zum Aufräumen".** Fügst du ein AK in der Mitte ein, verschieben sich die
Folgenummern — das ist ein echter inhaltlicher Diff und in Ordnung. Ohne Einfügung wird nicht
umnummeriert.

## Format-Fallen

Jira speichert Beschreibungen als ADF oder Wiki-Markup, GitHub und Linear als Markdown. Arbeite
in dem Format, das dir der Tracker liefert, und schreibe in dem, das er erwartet. Wandelst du
ADF nach Markdown, änderst drei Wörter und schreibst Markdown zurück, ist der Diff so gross wie
das Feld — konvertiert wurde jede Zeile.

Wenn der in dieser Session verfügbare Zugang zwangsläufig konvertiert, ist ein Format-Diff
unvermeidbar. Sag das dem User, bevor du schreibst, und lass ihn entscheiden. Ein
angekündigter Grossdiff ist etwas anderes als ein unerwarteter.

## Ausnahme: einmalige Normalisierung

Weicht der Bestand strukturell vom Golden Example ab (Prosa-Ticket, fehlende Sektionen, AKs im
Fliesstext), dann ist die Überführung in die Golden-Example-Struktur selbst die beauftragte
Änderung. Dieser eine grosse Diff ist legitim. Damit er nachvollziehbar bleibt:

- **Umhängen, nicht umschreiben.** Jeder Bestandssatz wandert wortgleich in die passende
  Sektion. Umformuliert wird nur, was der Auftrag inhaltlich ändert. Wer den Diff liest, soll
  seine eigenen Sätze wiedererkennen.
- **Nichts entsorgen.** Inhalt, der in keine Golden-Example-Sektion passt, bleibt als eigener
  Abschnitt am Ende stehen — oder du fragst den User, wohin damit. Stillschweigendes Weglassen
  ist der teuerste Fehler in dieser Phase, weil es im Diff wie Aufräumen aussieht.
- **Getrennt berichten.** Im Bericht die Strukturänderung und die inhaltlichen Änderungen
  getrennt ausweisen, damit der Leser nicht beides gleichzeitig entwirren muss.
- **Nur einmal.** Ab dem zweiten Anfassen ist die Struktur konform. Jeder weitere Grossdiff auf
  demselben Ticket ist ein Fehler, keine Normalisierung.

## Nebenfelder und Kommentare

Titel, Labels, Links, Status, Schätzung und Zuweisung nur ändern, wenn es beauftragt ist — auch
sie erzeugen Protokolleinträge, die jemand liest. Bestehende Kommentare nie editieren; ein
Kommentar ist die Äusserung einer Person zu einem Zeitpunkt.

## Beispiel

Bestand (`before`, Auszug):

```
Acceptance Criteria
1. Der Nutzer kann die Liste seiner Zuweisungen öffnen
2. Der Nutzer kann eine Zuweisung entfernen
3. Der Nutzer sieht eine Bestätigung
4. Der Nutzer kann die Liste filtern

Dev Notes
- Endpoint /assignments existiert bereits
```

Auftrag: "AK 3 ist zu vage — die Bestätigung muss den entfernten Eintrag benennen."

Richtig (`diff -u before after`):

```
-3. Der Nutzer sieht eine Bestätigung
+3. Der Nutzer sieht eine Bestätigung, die den entfernten Eintrag benennt
```

Eine Zeile raus, eine rein. AK 1, 2 und 4 stehen zeichengleich, "Nutzer" bleibt "Nutzer", die
Striche in den Dev Notes bleiben Striche, die Sektion bleibt vorhanden.

Falsch (Full-Replace mit Politur): AKs auf "Der USER kann …" umformuliert, Dev Notes entfernt
weil nicht im Golden Example, Sektionsnamen auf Deutsch vereinheitlicht. Ergebnis: acht
geänderte Zeilen für eine inhaltliche Änderung — und der PO kann im Protokoll nicht mehr sehen,
was du eigentlich gemacht hast.
