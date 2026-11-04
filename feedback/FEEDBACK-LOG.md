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

## #16 Kern-Bereitstellung der Story als Postcondition statt als AK 1

- **Datum / Artefakt:** 04.11.2026 · Story (Doc-Kommentar)
- **Bereich:** Postconditions
- **Was der Skill tat:** Eine Enabler-nahe Business-Story verlangte im Kern, dass das SYSTEM eine neue Organisationseinheit in einer bestehenden Hierarchie bereitstellt, neben einer bestehenden Einheit. Die Bereitstellung passiert bei Auslieferung, ohne User-Interaktion. Der Skill schrieb sie als Postcondition 1: «Das SYSTEM stellt die neue Organisationseinheit unter [übergeordneter Einheit] auf derselben Hierarchiestufe wie [bestehende Einheit] bereit». Die AKs beschrieben nur, was der USER danach getrennt überblicken kann und wie das SYSTEM die Einheiten danach behandelt. Phase 4 meldete das nicht.
- **Feedback:** «Hier auch wieder … das zentrale Element, welches von der Story gefordert wird, kann keine Postcondition sein. Es ist ein AK.» Dazu der Wunsch, den Fall als Log für die Verbesserung des Skills festzuhalten.
- **Regel-Vorschlag:** Was die Story im Kern fordert, ist AK 1, auch wenn das SYSTEM es ohne User-Aktion herstellt (Bereitstellung bei Auslieferung, Migration, Seed). Postconditions tragen nur Folgen und Nebenwirkungen dieses Kerns, z.B. wie sich Sichtbarkeit, Zuweisung oder Versand danach verhalten. Prüffrage pro Postcondition: «Wäre die Story ohne diesen Satz noch dieselbe Story?» Nein heisst AK. Gleiches Muster wie #13 (Recht als Postcondition), dort für Rechte, hier für jede Art Bereitstellung. Die Ursache liegt vermutlich in der Faustregel «AK = USER handelt, Postcondition = SYSTEM reagiert», die SYSTEM-Bereitstellungen ohne Auslöser in die Postconditions drückt. Für Phase 4: Prüfpunkt «Kern der Story steht in den Postconditions» aufnehmen. Wiederholt sich innerhalb eines Tages, Priorität hoch.
- **Status:** offen

## #15 Ausnahme als eigene Postcondition statt in die Regel eingebaut

- **Datum / Artefakt:** 04.11.2026 · Story (Doc-Kommentar)
- **Bereich:** Postconditions
- **Was der Skill tat:** Die Story legte fest, wer eine Benachrichtigung erhält. Der Skill schrieb dazu zwei Postconditions. Die erste war die positive Regel: «Das SYSTEM versendet die Benachrichtigung an alle User, die sie abonniert haben, WENN ein USER einen Eintrag mit Bemerkung erstellt oder ändert». Die zweite schränkte nur ein: «Das SYSTEM versendet die Benachrichtigung nicht an den USER, der den Eintrag erstellt oder geändert hat». Die zweite Postcondition engt also nur den Empfängerkreis der ersten ein. Phase 4 meldete das nicht.
- **Feedback:** Der User fragte, ob die zweite eine Einengung der ersten ist. Wenn ja, solle der Skill eine klare Anforderung schreiben und die Regel nicht unnötig aufsplitten, «in sowas wie hinreichende und notwendige Bedingung». Das sei ein häufiges Muster, das vermieden werden soll: «Es ist schwierig zu lesen und stiftet Verwirrung beim Team.»
- **Regel-Vorschlag:** Eine Regel steht in einem einzigen AK oder einer einzigen Postcondition, inklusive ihrer Ausnahmen. Ein zweiter Satz, der nur sagt, wann die Regel des ersten NICHT gilt («… nicht an …», «… ausser …», «… jedoch nicht, WENN …»), wird in den ersten eingebaut, z.B. «an alle anderen User, die sie abonniert haben, WENN der USER …». Prüffrage: «Ist dieses AK oder diese Postcondition nur dann verständlich, wenn man ein anderes daneben liest?» Ja heisst zusammenführen. Abzugrenzen vom Duplikat-Test: Dort sind zwei Sätze redundant, hier ergänzen sie sich und gehören darum zusammen. Für Phase 4: Prüfpunkt «Einschränkung ohne eigene Regel, als separater Satz zu einer anderen Regel» aufnehmen.
- **Status:** offen

## #14 Vorschlag des Users ungeprüft übernommen: Precondition gestrichen, ohne die ein Recht nutzlos ist

- **Datum / Artefakt:** 04.11.2026 · Story (Doc-Kommentar, drei Runden)
- **Bereich:** Preconditions
- **Was der Skill tat:** Eine Story führte ein Download-Recht für Einträge ein. Die Precondition lautete «Der USER hat das Recht, die Einträge seiner und aller untergeordneten Organisationen anzuzeigen». Der User fragte, ob diese Precondition müssig sei: Ein natürlicher User brauche sie über die Oberfläche, ein technischer User nicht zwingend, und eine Trennung mache es kompliziert. Der Skill stimmte zu («Ich sehe es wie du»), begründete, dass das Download-Recht und die Organisationseinschränkung als System-Constraints jeden Zugriffsweg abdeckten, und strich die Precondition auf ein «ja». Danach schlug der User vor, das Anzeige-Recht als Lösungshinweis festzuhalten, und der Skill legte dafür einen Abschnitt an.
- **Feedback:** «Wie will aber der technische User herausfinden, welche Datei er downloaden kann, wenn er diese nicht abfragen kann … er ist ja dann blind … Bitte Precondition mit Recht wiederherstellen und diese Anmerkung hier entfernen.» Und: «Warum bist du hier nicht selbst darauf gekommen … ist eigentlich logisch, oder?»
- **Regel-Vorschlag:** Bevor eine Precondition gestrichen wird, prüfen, ob die AKs ohne sie überhaupt ausführbar sind: Kann der Akteur das Objekt der Aktion finden, auswählen oder identifizieren, ohne die vorausgesetzte Fähigkeit? Ein Recht auf eine Aktion an einem Objekt (herunterladen, ändern, löschen) setzt voraus, dass der Akteur das Objekt sehen oder abfragen kann. Das gilt für jeden Zugriffsweg, auch für technische User. Eine Überlegung des Users zu einer Precondition ist eine Prüffrage, keine Entscheidung: Erst die Ausführbarkeit prüfen, dann zustimmen oder widersprechen. Zustimmung ohne Prüfung ist hier der eigentliche Fehler. Für Phase 4: Prüfpunkt «Ist jede Aktion in den AKs ohne die Preconditions ausführbar, inklusive Auffinden des Objekts?» aufnehmen. Verwandt mit der Herkunftsregel: Sie prüft, woher eine Precondition kommt, aber nicht, ob die Story ohne sie trägt.
- **Status:** offen

## #13 Neu eingeführtes Recht als Postcondition statt als erstes AK

- **Datum / Artefakt:** 04.11.2026 · Story (Doc-Kommentar)
- **Bereich:** Postconditions
- **Was der Skill tat:** Die Story setzte ein Recht als Precondition voraus, das im System nicht existiert. Der Skill erkannte das korrekt und liess die Story das Recht selbst einführen. Er folgte dabei Beispiel 1 im Golden Example: ein Constraint-AK «Das SYSTEM lässt den Download nur für USER zu, denen die Berechtigung dafür zugewiesen ist» am Ende der AK-Liste und eine Postcondition «Das SYSTEM stellt die Berechtigung … in der Rollenverwaltung zur Zuweisung bereit». Die übrigen AKs sprachen vom «USER» ohne Bezug auf das Recht.
- **Feedback:** «Ich sehe das nicht als Postcondition … dies muss ja als erstes gemacht werden, bevor der berechtigte User dann die Aktionen ausführen kann.» Im selben Durchgang: «Hier würde ich eben dann ‹der berechtigte USER› schreiben.» Dazu der Wunsch, das auch für die Verbesserung des Skills festzuhalten.
- **Regel-Vorschlag:** Führt eine Story ein Recht ein, steht die Bereitstellung des Rechts als AK 1, nicht als Postcondition: Sie ist Voraussetzung für alle folgenden AKs, kein Ergebnis einer User-Aktion. Die folgenden AKs sprechen vom «berechtigten USER». Ein zusätzliches Constraint-AK «nur für USER mit zugewiesener Berechtigung» entfällt dann als Implikat. Golden Example Beispiel 1 und die Herkunftsregel («Constraint-AK plus Postcondition») widersprechen dem und sind entsprechend anzupassen. Für Phase 4: Prüfpunkt «Recht als Postcondition statt AK 1» aufnehmen.
- **Status:** offen

## #12 Abgrenzung verweist auf die Story, die es umsetzt

- **Datum / Artefakt:** 04.11.2026 · Story (Doc-Kommentar)
- **Bereich:** Out of Scope
- **Was der Skill tat:** Die Abgrenzung enthielt «Das SYSTEM zeigt keine Änderungshistorie der Werte an; das leistet [andere Story]» und «Das SYSTEM prognostiziert keine Werte und stellt sie nicht als Zeitreihe dar; das leistet [andere Story]». Beide Punkte stammten aus einer früheren Fassung. Der Skill hatte sie beim Refinement übernommen, obwohl die Skill-Regel solche Nachbar-Verweise bereits ausschliesst («Dass etwas in einem anderen Epic steckt, ist kein Out-of-Scope-Punkt»). Phase 4 meldete es nicht.
- **Feedback:** «Ich glaube, das haben wir schon mehrmals besprochen … Ich möchte nicht, dass du auf Storys verweist, die etwas umsetzen, das hier nicht umgesetzt wird … eine andere Story setzt immer etwas um, das diese Story nicht umsetzt, ansonsten werden es nicht zwei Storys. Das verwirrt höchstens oder schlägt Brücken zu anderen Geschichten, die dann Diskussionen hervorbringen, die nicht geführt werden sollen.»
- **Regel-Vorschlag:** Abgrenzungen nennen nie eine andere Story als Ort der Umsetzung, weder als Ticketnummer noch als «das leistet …», «folgt in …» oder «siehe …». Eine Abgrenzung, deren einziger Inhalt ist, dass eine Nachbar-Story etwas liefert, wird ganz gestrichen, nicht nur ihr Verweis. Die bestehende Regel gilt ausdrücklich auch für Bestand: Beim Refinement einer bestehenden Story die Abgrenzungen aktiv auf solche Verweise durchsuchen und sie entfernen, statt sie zu übernehmen, auch wenn sie im Ticket schon stehen. Für Phase 4: «Abgrenzung verweist auf Nachbar-Story» als festen Prüfpunkt aufnehmen. Das Muster wurde laut User schon mehrfach besprochen und tritt trotz Regel wieder auf, Priorität hoch.
- **Status:** offen

## #11 Einsehen-AK neben einem Ändern-AK für dieselben Akteure

- **Datum / Artefakt:** 04.11.2026 · Story (Doc-Kommentar, unmittelbar nach #10)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** In derselben Story stand nach dem Streichen aus #10 weiterhin das AK «Der USER der Prüfstelle kann die Werte samt Typ in der Detailansicht einsehen». Ein anderes AK sagte bereits: «Das SYSTEM lässt das Ändern der Werte für alle USER zu, mit deren Organisation der Eintrag geteilt ist». Der Eintrag ist immer mit der Prüfstelle geteilt, und die Precondition nennt die Detailansicht. Wer ändern darf, sieht die Werte zwangsläufig. Phase 4 meldete das nicht, und der Skill übersah es beim Korrigieren von #10, obwohl derselbe Kommentar-Durchgang lief.
- **Feedback:** «Auch dieses AK ist eigentlich schon im oberen AK enthalten … wenn er gemäss Precondition die Detailansicht anzeigt und es gemäss dem anderen AK ändern kann, und zwar alle Organisationen, mit denen der Eintrag geteilt ist, besagt das nichts anderes … unnötige Doppelung … Das müssen wir unbedingt verbessern.»
- **Regel-Vorschlag:** Berechtigungs-AKs implizieren die schwächeren Fähigkeiten: Wer ändern darf, kann einsehen; wer löschen darf, kann den Eintrag finden. Ein separates «kann einsehen»-AK für einen Akteur, den ein «darf ändern»-AK schon einschliesst (direkt oder über «alle, mit denen geteilt ist»), ist ein Implikat und wird gestrichen. Vor dem Streichen prüfen, ob das Einsehen-AK etwas Eigenes trägt (hier «samt Typ»), und dieses Eigene, falls nötig, in ein bestehendes AK verlagern statt ein Duplikat zu behalten. Wenn ein User ein Duplikat meldet, die ganze AK-Liste sofort auf weitere Fälle desselben Musters prüfen, nicht nur die markierte Stelle. Für Phase 4: Implikationstest «Berechtigung schliesst Anzeige ein» als festen Prüfpunkt aufnehmen. Folgt auf #10.
- **Status:** offen

## #10 AK wiederholt Precondition und ein anderes AK

- **Datum / Artefakt:** 04.11.2026 · Story (Doc-Kommentar)
- **Bereich:** AK-Formulierung
- **Was der Skill tat:** Die Story hatte als Precondition «Der USER erfasst einen Eintrag oder zeigt einen bestehenden Eintrag im Detail an». Ein AK sagte schon, dass der USER vorbelegte Werte übernehmen oder ändern kann. Trotzdem stand als weiteres AK «Der USER kann die Werte in der Detailansicht des Eintrags anzeigen und ändern». Das AK war aus der Vorgänger-Fassung übernommen. Phase 4 hat es nicht als Duplikat gemeldet.
- **Feedback:** «Hier steht eigentlich schon in der Precondition, dass der User die Detailansicht anzeigen muss. Und es steht auch in den AKs, dass er die Werte ändern kann. Warum also ein erneutes AK, das die Precondition und das vorherige AK wieder aufnimmt? Das neue hat gar keinen Mehrwert.»
- **Regel-Vorschlag:** Vor dem Ausgeben jedes AK gegen die Preconditions UND die übrigen AKs prüfen, nicht nur AK gegen AK. Ein AK, dessen Ort aus einer Precondition folgt («in der Detailansicht», wenn die Precondition die Detailansicht nennt) und dessen Fähigkeit schon ein anderes AK trägt («ändern»), ist redundant und wird gestrichen. Gilt besonders für AKs, die aus einer früheren Fassung übernommen werden: Bei jeder Überarbeitung den Duplikat- und Implikations-Litmus erneut über die ganze Liste laufen lassen. Für Phase 4: Den Tester- und Architekten-Prüfauftrag um «AK wiederholt Precondition plus anderes AK» ergänzen. Verwandt mit der bestehenden Regel «keine Wiederholung einer Precondition als Qualifier im AK».
- **Status:** offen

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
