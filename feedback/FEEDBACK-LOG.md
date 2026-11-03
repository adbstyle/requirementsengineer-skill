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

## #9 Lösungsmechanik trotz bekanntem Feedback, und ein Ortsbezug als Rest

- **Datum / Artefakt:** 03.11.2026 · Story (Doc-Kommentar, zwei Runden)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Eine Story für eine Übersichtsansicht hatte das AK «Der USER kann von einem Eintrag in der Übersicht zur Detailansicht des Eintrags wechseln». Das ist genau das Muster aus #5, obwohl #5 schon im Log stand. Phase 4 meldete es nicht. Auf den ersten Hinweis formulierte der Skill um zu «Der USER kann zu den Einträgen in der Übersicht Detailinformationen anzeigen». Damit blieb die Mechanik weg, aber «in der Übersicht» liess sich als Ort der Anzeige lesen.
- **Feedback:** Runde 1: «Das hier ist wieder Lösung … du schreibst vor, dass er zur Detailansicht navigieren kann … diesen Fall haben wir im Feedback-Log schon dokumentiert.» Runde 2: «‹in der Übersicht› lässt immer noch die Interpretation zu, dass dies eben in der Übersicht geschehen soll … die Idee ist, dass er diese finden bzw. zu dieser navigieren kann … ob die Anzeige auf, über oder in der Detailseite geschieht, soll offen bleiben.» Neu: «Der USER kann von der Übersicht aus zu jedem angezeigten Eintrag Detailinformationen erreichen».
- **Regel-Vorschlag:** Wenn ein AK von einer Ansicht aus auf weitere Information verweist, wird die Ansicht nur als Ausgangspunkt genannt («von der Übersicht aus»), nie als Ort der Anzeige («in der Übersicht … anzeigen»). Das Verb heisst «erreichen» oder «finden», nicht «anzeigen», «wechseln» oder «navigieren». Litmus aus #5 erweitern: Bleibt die Anforderung erfüllt, wenn die Details direkt in der Ausgangsansicht, in einem Overlay oder in einer eigenen Ansicht erscheinen? Und lässt der Wortlaut alle drei zu, ohne dass einer naheliegt? Ausserdem gehören die offenen Log-Einträge als Prüfpunkte in Phase 4, sonst wiederholt sich ein bereits gemeldetes Muster. Verwandt mit #5 und #8.
- **Status:** offen

## #8 Erfolgskriterium nimmt den Einstiegsflow vorweg

- **Datum / Artefakt:** 02.11.2026 · Epic (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Das Erfolgskriterium lautete «ADMINs, KOs und USER gelangen nach dem Login auf eine Startseite mit den Inhalten ihrer Rolle». Die Formulierung stammte aus dem Story-Satz der Vorlage («nach dem Login ein Dashboard/eine Startseite sehen»). Damit legte der Skill fest, wann und wo die Ansicht erscheint: direkt nach dem Login, als Einstiegsseite. Die Folgekriterien hingen am Ort («erkennen auf der Startseite …»), und der Story-Satz übernahm «nach dem Login». In Phase 4 hat keiner der sechs Prüf-Agenten das als Übersteuerung gemeldet.
- **Feedback:** «Das ist zuviel Lösung … mit diesem EK nimmst du einen Userflow vorweg … es reicht einfach, dass sie ein Dashboard anzeigen können … vielleicht entscheidet der UXler anders … ich will ihm als RE den Flow nicht vorgeben … es sei denn, der PO will es so, dann erhältst du das als explizite Anforderung.» Neu: «… können ein Dashboard mit den Inhalten ihrer Rolle anzeigen». «Nach dem Login» und «Startseite» sind überall gestrichen.
- **Regel-Vorschlag:** Erfolgskriterien und AKs fordern, dass der USER eine Ansicht anzeigen kann, nicht wann oder wodurch sie erscheint. Auslöser und Einstiegspunkte wie «nach dem Login», «beim Öffnen», «als Startseite», «landet auf» oder «wird weitergeleitet» sind Userflow und damit UX-Entscheid. Eine Formulierung aus der Vorlage (Story-Satz, Kundenbemerkung) ist kein Auftrag, den Flow festzuschreiben. Nur eine ausdrückliche Vorgabe des PO macht ihn zur Anforderung. Litmus: Wäre die Anforderung auch erfüllt, wenn die Ansicht über die Navigation statt automatisch nach dem Login erreichbar ist? Wenn ja, den Auslöser streichen. Gilt auch für Folgekriterien, die den Ort referenzieren («auf der Startseite»). Verwandt mit #5 und #6. Für Phase 4: Der UX-Prüfauftrag sollte Einstiegs- und Flow-Vorgaben ausdrücklich als Übersteuerung nennen.
- **Status:** offen

## #7 «kann alle X anzeigen» in einer begrenzten Darstellung

- **Datum / Artefakt:** 02.11.2026 · Story (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Eine Story für eine Kalenderdarstellung hatte das AK «Der ADMIN kann alle Einträge eines Tages anzeigen». Der Skill wollte damit die Lehre aus #1 umsetzen («kann alle anzeigen» statt «sieht alle»). Ein Kalendertag hat aber nur begrenzten Platz.
- **Feedback:** «Was ist, wenn wir 100 Einträge genau gleichzeitig von 10 bis 14 Uhr an einem Tag haben … hier ist das ‹alle› wieder ein Problem … wird so nicht möglich sein … brauchen hier eine allgemeine Formulierung.» Neu lautet das AK: «Der ADMIN erkennt, wie viele Einträge an einem Tag stattfinden, und kann jeden davon anzeigen».
- **Regel-Vorschlag:** In einer Darstellung mit begrenztem Platz (Kalendertag, Kachel, Karte, Zelle) nicht «alle X anzeigen» verlangen, auch nicht mit «kann». Stattdessen zwei Dinge fordern: Die Menge ist erkennbar, und jedes Element bleibt einzeln erreichbar. Litmus: Bei einem Extremwert (100 gleichzeitige Einträge) ehrlich prüfen, ob das AK noch erfüllbar ist, ohne eine bestimmte Lösung zu erzwingen. Wenn nein, auf «Menge erkennbar plus jedes Element erreichbar» umformulieren. Ergänzt #1, das für Listen mit Paging gilt.
- **Status:** offen

## #6 Vertraglich zulässige Lösung als Anforderung formuliert

- **Datum / Artefakt:** 02.11.2026 · Epic (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Das Erfolgskriterium lautete «Die angezeigte Ansicht lässt sich über den Druckdialog des Browsers drucken und als PDF speichern». Die Vorlage war eine Requirement-Abgrenzung («keine Druckoptimierung über den Browser-Standard hinaus»). Die Abgrenzung erlaubt den Browser-Druck als Lösung, der Skill machte daraus die geforderte Lösung. Zwei Prüf-Agenten hatten den Mechanismus in Phase 4 sogar ausdrücklich als «vertraglich bedingt, keine Übersteuerung» gebilligt.
- **Feedback:** «Hier gleiches … das ist eine Lösung … die Anforderung soll genereller geschrieben werden, so dass diese Lösung unter der Anforderung zulässig ist … aber wir wollen die Lösung nicht zur Anforderung machen.» Neu: «Die angezeigte Ansicht kann gedruckt oder als PDF gespeichert werden».
- **Regel-Vorschlag:** Eine Abgrenzung oder Vorgabe, die eine Lösung erlaubt oder begrenzt, gehört in Out of Scope, nicht als Weg in die Anforderung. Die Anforderung bleibt so allgemein, dass die erlaubte Lösung sie erfüllt, ohne sie zu verlangen. Litmus: Würde eine andere, ebenfalls zulässige Lösung die Anforderung verfehlen, nur weil der Satz den Weg nennt («über X», «mittels Y», «via Z»)? Wenn ja, den Weg streichen. Für Phase 4: Billigt ein Prüf-Agent einen Mechanismus als «vertraglich bedingt», ist das kein Grund, ihn in der Anforderung zu lassen. Er gehört dann in Out of Scope oder in eine Anmerkung. Verwandt mit #5.
- **Status:** offen

## #5 Erfolgskriterium nimmt die Navigation zu einer Detailseite vorweg

- **Datum / Artefakt:** 02.11.2026 · Epic (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Das Erfolgskriterium lautete «Aus der Übersicht gelangen ADMINs zur Detailseite eines Eintrags». Damit war festgelegt, dass die Details auf einer eigenen Detailseite stehen und per Navigation erreicht werden. Die Vorlage stammte aus einer Requirement-Abgrenzung («keine Aktionen über die Navigation zur Detailseite hinaus») und aus dem Wissen, dass es eine solche Seite bereits gibt.
- **Feedback:** «Das hier ist eine Lösungsbeschreibung … du nimmst vorweg, dass Details auf der Detailseite angezeigt werden … ist aber nicht nötig … wir bleiben beim Was, und das meint, dass der ADMIN zu den angezeigten Einträgen Detailinformationen finden/anzeigen kann.» Neu: «ADMINs können zu den in der Übersicht angezeigten Einträgen Detailinformationen anzeigen».
- **Regel-Vorschlag:** Erfolgskriterien und AKs beschreiben, welche Information der USER erreichen kann, nicht wo sie steht oder wie er dorthin gelangt. Begriffe wie «Detailseite», «Seite», «Dialog», «navigiert zu», «gelangt zu» und «verlinkt auf» sind Lösungsmechanik. Litmus: Bleibt die Anforderung erfüllt, wenn die Details in einem Overlay, einer Seitenleiste oder direkt im Eintrag erscheinen? Wenn ja, das Wo streichen und das Was formulieren («kann zu X Detailinformationen anzeigen»). Das gilt auch, wenn die Codebase oder eine Requirement-Abgrenzung die Lösung bereits nennt: Kontextwissen aus Phase 2 ist kein Grund, die Lösung in die Anforderung zu schreiben. Die bestehende Anti-Pattern-Liste nennt «Mechanik der Lösung» nur für AKs, nicht ausdrücklich für Erfolgskriterien auf Epic-Ebene.
- **Status:** offen

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
