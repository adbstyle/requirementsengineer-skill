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
