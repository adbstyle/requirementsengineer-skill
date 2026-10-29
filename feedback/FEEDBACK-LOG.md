# Feedback-Log requirementsengineer-Skill

Sammelt Feedback zum Skill aus allen Projekten, damit nach einigen Einträgen Muster sichtbar werden und der Skill gezielt verbessert werden kann. Liegt bewusst ausserhalb von `skills/` und wird nicht mit dem Skill ausgeliefert.

## So wird erfasst

Ein Eintrag pro Feedback, neueste zuoberst, fortlaufende Nummer. Der Wortlaut des Users wird sinngemäss oder als Zitat festgehalten, nicht interpretiert. Die abgeleitete Regel ist ein Vorschlag, bis sie im Skill steht.

**Anonym erfassen.** Das Repository ist öffentlich. Keine Projekt-, Kunden-, Organisations- oder Personennamen, keine Issue- oder Story-Nummern, keine Story-Titel. Fachbegriffe, die auf ein Projekt schliessen lassen, durch neutrale ersetzen (Rollen wie USER/ADMIN, Objekte wie «Eintrag»). Gelernt wird aus dem Muster, nicht aus dem Projekt: Das Beispiel bleibt nur so konkret, dass die Regel nachvollziehbar ist.

Felder:
- **Datum / Artefakt:** wann und an welcher Art Artefakt es auftrat (Story, Epic, Doc-Kommentar), ohne Namen oder Nummer
- **Bereich:** eine Kategorie aus der Liste unten, damit sich Einträge gruppieren lassen
- **Was der Skill tat:** das konkrete Ergebnis, das Anlass gab
- **Feedback:** was der User gesagt hat
- **Regel-Vorschlag:** wie der Skill es künftig machen sollte
- **Status:** offen · im Skill übernommen (mit Commit) · verworfen (mit Grund)

Bereiche: Satzschablone · Preconditions · AK-Formulierung · Postconditions · Out of Scope · Offene Fragen · Story-Schnitt · Phase 2 Kontext · Phase 4 Validierung · Rückfragen · Tracker-Writeback · Output/Format

## Auswertung

Bei der Auswertung Einträge nach Bereich gruppieren und fragen: Wiederholt sich dasselbe Problem? Widerspricht eine bestehende Skill-Regel dem Feedback? Wo hätte ein Litmus-Test im Skill den Fehler verhindert?

---

## #4 AK aus der Schwester-Story übernommen, obwohl ein anderes AK ihn schon impliziert

- **Datum / Artefakt:** 29.10.2026 · Story (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Die Story (USER erfasst) übernahm aus einer parallel geschnittenen Schwester-Story (ADMIN erfasst) das AK «Das SYSTEM lässt das Erfassen nur zu publizierten und archivierten Einsätzen zu». In der Schwester-Story ist es nötig, weil ADMIN auch ohne Zuweisung erfassen und sonst Entwürfe wählbar wären. In dieser Story sagt AK 1 «nur zu einem Einsatz, dem er zugewiesen ist». Zuweisen geht laut einer Nachbar-Story aber nur bei publizierten Einsätzen, und archivierte behalten ihre Zuweisungen. Das Status-AK war damit leer.
- **Feedback:** «Ist das nicht überflüssig zu erwähnen, weil bei einem Entwurf gar kein USER zugewiesen werden kann?» AK gestrichen.
- **Regel-Vorschlag:** Werden Stories nach Rolle geschnitten (SPIDR «nach User-Rolle») und eine aus der anderen abgeleitet, prüft der Skill jedes übernommene AK neu im Kontext der neuen Rolle. Litmus: Folgt die Regel schon aus einem anderen AK dieser Story zusammen mit einer Regel der einführenden Nachbar-Story (hier Zuweisung nur bei publizierten Einsätzen)? Wenn ja, weglassen. Ein AK, das in der Schwester-Story eine Lücke schliesst, kann in der abgeleiteten Story leer sein. Verwandt mit #2 und #3 (Redundanz).
- **Status:** offen

## #3 Postconditions, die Selbstverständliches oder anderswo Geregeltes wiederholen

- **Datum / Artefakt:** 29.10.2026 · Story (zwei Doc-Kommentare)
- **Bereich:** Postconditions
- **Was der Skill tat:** Zwei Postconditions bestätigten nur, was schon feststand:
  - «Das SYSTEM führt den erfassten Eintrag als eigenen Eintrag neben bestehenden Einträgen derselben Person zum selben Einsatz». Das sagen bereits ein AK der Story und das Glossar («mehrere Einträge pro Person und Einsatz sind möglich»).
  - «Das SYSTEM behandelt einen beim Erfassen als kontrolliert markierten Eintrag wie jeden anderen kontrollierten Eintrag». Was «kontrolliert» bewirkt, regeln eine Nachbar-Story und das Glossar.
  Beide waren als Antwort auf Findings aus dem perspektivenbasierten Lesen entstanden (Tester: «Endzustand prüfbar?», BA: «Redundanz»).
- **Feedback:** «Was denn sonst … es stimmt, aber ist es nötig, dies zu sagen?» und zur zweiten: «gleiches hier». Beide gestrichen.
- **Regel-Vorschlag:** Eine Postcondition muss einen Zustand beschreiben, den diese Story neu herbeiführt und der nicht schon aus einem AK, dem Glossar oder einer Nachbar-Story folgt. Litmus pro Postcondition:
  1. Gibt es eine plausible Alternative, die ein Team ohne diesen Satz umsetzen würde? Wenn nein, streichen.
  2. Wiederholt sie ein AK dieser Story oder eine Regel, die eine andere Story einführt? Wenn ja, streichen.
  Ergänzend für Phase 4: Findings der Art «Verhalten X ist hier nicht explizit» nicht mit einer neuen Postcondition beantworten, wenn X in der einführenden Story oder im Glossar steht. Das passt zum Unabhängigkeits-Filter.
- **Status:** offen

## #2 Positives und negatives AK für dieselbe Regel

- **Datum / Artefakt:** 29.10.2026 · Story (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Zwei aufeinanderfolgende AKs drückten dieselbe Regel aus. AK 4 lautete «Der ADMIN kann den Eintrag für eine Person aus dem berechtigten Personenkreis des Angebots erfassen, auch wenn …». AK 5 lautete «Der ADMIN kann keinen Eintrag für eine Person erfassen, die dem berechtigten Personenkreis des Angebots nicht angehört».
- **Feedback:** «Ist das nicht dasselbe, einmal positiv und einmal negativ ausgedrückt?»
- **Regel-Vorschlag:** Eine Regel wird in genau einem AK formuliert. Die Abgrenzung kommt mit «nur» in dasselbe AK, statt ein zweites, verneintes AK anzuhängen. Beispiel: «Der ADMIN kann den Eintrag nur für … erfassen». Litmus vor jedem «kann nicht»- oder «lehnt ab»-AK: Ist es die Umkehrung eines anderen AKs? Wenn ja, mit «nur» zusammenlegen. Eigenständig bleibt ein Negativ-AK nur, wenn es einen Fall abdeckt, den kein positives AK berührt.
- **Status:** offen

## #1 «sieht alle» statt «kann alle anzeigen»

- **Datum / Artefakt:** 29.10.2026 · Story (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** AK 1 lautete «Der USER sieht alle eigenen Einträge … in einer gemeinsamen Übersicht». Das folgte der Konvention bestehender Projekt-Stories.
- **Feedback:** «Alle» meint alle, auch 10'000. Die sieht man nicht einfach, aber man kann sie sehen. Die Lösung wird paginieren, also sieht der User nie alle, er kann aber alle sehen.
- **Regel-Vorschlag:** Listen- und Übersichts-AKs als Möglichkeit formulieren: «Der USER kann alle X … anzeigen», nicht als Zustand «Der USER sieht alle X». Litmus: Wäre das AK bei Paginierung formal noch erfüllt?
- **Status:** offen
