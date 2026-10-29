# Feedback-Log requirementsengineer-Skill

Sammelt Feedback zum Skill aus allen Projekten, damit nach einigen Einträgen Muster sichtbar werden und der Skill gezielt verbessert werden kann. Liegt bewusst ausserhalb von `skills/` und wird nicht mit dem Skill ausgeliefert.

## So wird erfasst

Ein Eintrag pro Feedback, neueste zuoberst, fortlaufende Nummer. Der Wortlaut des Users wird sinngemäss oder als Zitat festgehalten, nicht interpretiert. Die abgeleitete Regel ist ein Vorschlag, bis sie im Skill steht.

Felder:
- **Datum / Projekt / Artefakt:** wo es auftrat (Issue, Story, Doc)
- **Bereich:** eine Kategorie aus der Liste unten, damit sich Einträge gruppieren lassen
- **Was der Skill tat:** das konkrete Ergebnis, das Anlass gab
- **Feedback:** was der User gesagt hat
- **Regel-Vorschlag:** wie der Skill es künftig machen sollte
- **Status:** offen · im Skill übernommen (mit Commit) · verworfen (mit Grund)

Bereiche: Satzschablone · Preconditions · AK-Formulierung · Postconditions · Out of Scope · Offene Fragen · Story-Schnitt · Phase 2 Kontext · Phase 4 Validierung · Rückfragen · Tracker-Writeback · Output/Format

## Auswertung

Bei der Auswertung Einträge nach Bereich gruppieren und fragen: Wiederholt sich dasselbe Problem? Widerspricht eine bestehende Skill-Regel dem Feedback? Wo hätte ein Litmus-Test im Skill den Fehler verhindert?

---

## #3 Postconditions, die Selbstverständliches oder anderswo Geregeltes wiederholen

- **Datum / Projekt / Artefakt:** 29.10.2026 · Freiwilligenplattform Stadt Zürich · Epic #53, Story 4 «Rapport für Freiwillige erfassen» (zwei Doc-Kommentare)
- **Bereich:** Postconditions
- **Was der Skill tat:** Zwei Postconditions bestätigten nur, was schon feststand:
  - «Das SYSTEM führt den erfassten Rapport als eigenen Rapport neben bestehenden Rapporten derselben Person zum selben Einsatz». Das sagen bereits AK 11 und das Glossar («mehrere Rapporte pro Person und Einsatz sind möglich»).
  - «Das SYSTEM behandelt einen beim Erfassen als kontrolliert markierten Rapport wie jeden anderen kontrollierten Rapport». Was «kontrolliert» bewirkt, regeln die Nachbar-Story #175 und das Glossar.
  Beide waren als Antwort auf Findings aus dem perspektivenbasierten Lesen entstanden (Tester: «Endzustand prüfbar?», BA: «Redundanz»).
- **Feedback:** «Was denn sonst … es stimmt, aber ist es nötig, dies zu sagen?» und zur zweiten: «gleiches hier». Beide gestrichen.
- **Regel-Vorschlag:** Eine Postcondition muss einen Zustand beschreiben, den diese Story neu herbeiführt und der nicht schon aus einem AK, dem Glossar oder einer Nachbar-Story folgt. Litmus pro Postcondition:
  1. Gibt es eine plausible Alternative, die ein Team ohne diesen Satz umsetzen würde? Wenn nein, streichen.
  2. Wiederholt sie ein AK dieser Story oder eine Regel, die eine andere Story einführt? Wenn ja, streichen.
  Ergänzend für Phase 4: Findings der Art «Verhalten X ist hier nicht explizit» nicht mit einer neuen Postcondition beantworten, wenn X in der einführenden Story oder im Glossar steht. Das passt zum Unabhängigkeits-Filter.
- **Status:** offen

## #2 Positives und negatives AK für dieselbe Regel

- **Datum / Projekt / Artefakt:** 29.10.2026 · Freiwilligenplattform Stadt Zürich · Epic #53, Story 4 «Rapport für Freiwillige erfassen» (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Zwei aufeinanderfolgende AKs drückten dieselbe Regel aus. AK 4 lautete «Der ADMIN/KO kann den Rapport für eine*n Freiwillige*n aus dem Freiwilligenkreis des Angebots erfassen, auch wenn …». AK 5 lautete «Der ADMIN/KO kann keinen Rapport für eine Person erfassen, die dem Freiwilligenkreis des Angebots nicht angehört».
- **Feedback:** «Ist das nicht dasselbe, einmal positiv und einmal negativ ausgedrückt?»
- **Regel-Vorschlag:** Eine Regel wird in genau einem AK formuliert. Die Abgrenzung kommt mit «nur» in dasselbe AK, statt ein zweites, verneintes AK anzuhängen. Beispiel: «Der ADMIN/KO kann den Rapport nur für … erfassen». Litmus vor jedem «kann nicht»- oder «lehnt ab»-AK: Ist es die Umkehrung eines anderen AKs? Wenn ja, mit «nur» zusammenlegen. Eigenständig bleibt ein Negativ-AK nur, wenn es einen Fall abdeckt, den kein positives AK berührt.
- **Status:** offen

## #1 «sieht alle» statt «kann alle anzeigen»

- **Datum / Projekt / Artefakt:** 29.10.2026 · Freiwilligenplattform Stadt Zürich · Epic #53, Story 2 «Eigene Rapporte anzeigen» (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** AK 1 lautete «Der FW sieht alle eigenen Rapporte … in einer gemeinsamen Übersicht». Das folgte der Konvention bestehender Projekt-Stories.
- **Feedback:** «Alle» meint alle, auch 10'000. Die sieht man nicht einfach, aber man kann sie sehen. Die Lösung wird paginieren, also sieht der User nie alle, er kann aber alle sehen.
- **Regel-Vorschlag:** Listen- und Übersichts-AKs als Möglichkeit formulieren: «Der USER kann alle X … anzeigen», nicht als Zustand «Der USER sieht alle X». Litmus: Wäre das AK bei Paginierung formal noch erfüllt?
- **Status:** offen
