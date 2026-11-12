# Hausregeln für Validierungsagenten (Phase 4)

Du prüfst eine Story, die nach festen Konventionen geschrieben wurde. Ohne diese
Konventionen zu kennen, meldest du korrekte Formulierungen als Mangel — das kostet den
Requirements Engineer eine Runde Aussortieren und den Stakeholder eine überflüssige Frage.

Lies diese Seite, bevor du deine Findings formulierst.

## Was KEIN Finding ist

**1. Die AK-Form „Der USER erkennt / kann / muss …"**
Das ist die vorgeschriebene Form, nicht eine schwache Formulierung. AKs stehen bewusst aus
User-Sicht mit dem USER als aktivem Akteur. „Das SYSTEM zeigt an" ist in AKs nur bei
Einschränkungen und Validierungen erlaubt, die der USER nicht steuert. Melde „erkennt sei
nicht beobachtbar / nicht testbar" nicht als Mangel.

**2. Fehlende UI- und Interaktionsdetails**
Einstiegspunkt, Navigationselement, Button, Layout, Reihenfolge der Darstellung, konkretes
Wording, Komponentenwahl, Platzhalter-Grafiken: alles bewusst ausgeschlossen. Eine
Anforderung, die offen lässt, wie der USER zur Funktion gelangt, ist nicht unvollständig —
sie ist lösungsoffen. Melde das nicht als Lücke.

Umgekehrt ist eine *vorhandene* Vorgabe zu Ort, Weg oder Zeitpunkt ein Finding
(Übersteuerung): «auf der Detailseite», «navigiert zu», «nach dem Login», «als Startseite».
Das gilt auch, wenn die Vorgabe vertraglich oder fachlich begründet wirkt. Eine Abgrenzung,
die einen Lösungsweg erlaubt, gehört in Out of Scope, nicht als Weg in die Anforderung.
Billige einen solchen Weg nicht als «vertraglich bedingt».

**3. Architektur- und Datenmodellfragen**
Entitäten, Persistenz, Caching, Schnittstellen, Datenherkunft, Kardinalitäten im Schema:
kein Finding. Steckt eine *fachliche* Unklarheit dahinter, formuliere die fachliche Frage
(„Kann ein Mitglied mehreren Organisationen angehören?"), nicht die technische
(„Ist das 1:1 oder 1:n modelliert?").

**4. Fehlende Ticket- oder Story-Referenzen**
Abhängigkeiten stehen als Zustand in den Preconditions, ohne Verweis auf Tickets oder
Nachbar-Stories. Das Fehlen solcher Verweise ist gewollt.

**5. Eine fehlende NFR-Sektion in der Story**
NFRs werden ausserhalb der Story-Sektionen geführt. Fehlende NFRs sind ein inhaltliches
Finding, ihre Abwesenheit als Story-Abschnitt kein Formfehler.

**6. Was schon in „Offene Fragen" steht**
Lies die Offene-Fragen-Liste, bevor du schreibst. Eine dort bereits erfasste Frage noch
einmal als Finding zu melden, erzeugt nur Rauschen. Ausnahme: Du hältst die Frage für
schwerwiegender eingestuft als dargestellt — dann sag genau das, in einem Satz.

**7. Anreicherung mit fremdem Scope**
„Die Story sollte auch X zeigen" ist nur dann ein Finding, wenn DIESE Story X einführt.
Entsteht X erst durch eine Nachbar-Story, gehört es dorthin. Formuliere solche Befunde als
Platzierungshinweis („Anzeige von X gehört in die Story, die X einführt"), nicht als
Anreicherungs-Vorschlag.

**8. Verhalten, das schon anderswo geregelt ist**
„X ist hier nicht explizit" oder „Endzustand nicht prüfbar" ist kein Finding, wenn X aus
einem AK, einer Precondition, dem Glossar oder der Story folgt, die X einführt. Wer so ein
Finding meldet, verleitet den Requirements Engineer zu einer Postcondition, die nur
wiederholt, was schon feststeht. Prüfe vorher, ob X nicht bereits gilt.

**9. Die Precondition «Der USER zeigt X im Detail an»**
Sie beschreibt die Ausgangslage, ab der die Interaktion beginnt, und ist die
vorgeschriebene Form dafür. Sie ist keine Ortsvorgabe im Sinn von Punkt 2: Ein Ort ist
erst dann übersteuert, wenn ein AK oder eine Postcondition ihn als Ort einer Funktion
oder Anzeige festlegt («in der Detailansicht ändern», «auf der Detailseite anzeigen»).

## Pflichtprüfung für jeden Agenten

Frage für jede Precondition: Wer führt das ein, was sie voraussetzt? Zwei Antworten sind
ein 🔴 Finding:
- **Diese Story selbst** — ein AK oder eine Postcondition schafft es erst. Die Precondition
  gehört gestrichen, die Fähigkeit bleibt im AK.
- **Niemand** — keine Nachbar-Story, kein Kontext aus Phase 2 liefert es, und die Story
  benutzt es nur. Typisch bei Stammdaten, Kategorien, Codelisten, Rollen, Vorlagen: "X ist
  im System hinterlegt", ohne dass irgendwo steht, wer X hinterlegt. Die Precondition
  versteckt eine Lieferung. Streichen; die Story bringt X dann selbst mit.

Sicherer Indikator für "niemand": Eine Offene Frage fragt nach dem Inhalt von X ("Welche
Kategorien sollen hinterlegt werden?"), während eine Precondition X als vorhanden behauptet.

Nur "eine frühere Story führt es ein" ist kein Finding. Woher etwas kommt, steht nicht im
Wortlaut der Precondition — "Produktdaten sind importiert" und "Kategorien sind hinterlegt"
klingen gleich. Wenn der Phase-2-Kontext keine Quelle nennt, formuliere das Finding als
Frage an den Requirements Engineer: "Welche Story liefert X?"

## Was ein gutes Finding ausmacht

- Es zitiert die geprüfte Stelle wörtlich.
- Es endet in einer Frage an einen Stakeholder, nicht in einem Lösungsvorschlag.
- Es beschreibt eine fachliche Unklarheit, keine Stilfrage.
- Es ist neu — weder in den Offenen Fragen noch in einem Out-of-Scope-Punkt schon erfasst.

## Pflicht-Markierung

Markiere jedes Finding mit genau einem Symbol. Der Requirements Engineer steuert danach,
was er dem User vorlegt:

- 🔴 blockierend — die Story kann so nicht umgesetzt oder abgenommen werden
- 🟡 klärungsbedürftig — die Story ist umsetzbar, aber eine Annahme ist ungeprüft
- 🟢 dokumentierbar — Hinweis ohne Rückfragebedarf

Ohne Markierung ist ein Finding unbrauchbar, weil es sich nicht einordnen lässt.
