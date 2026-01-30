# INVEST-Prinzip für User Stories - Zusammenfassung

## Übersicht
Das INVEST-Akronym (von Bill Wake) beschreibt sechs wesentliche Attribute guter User Stories:

- **I**ndependent (Unabhängig)
- **N**egotiable (Verhandelbar)
- **V**aluable (Wertvoll)
- **E**stimatable (Schätzbar)
- **S**mall (Klein)
- **T**estable (Testbar)

---

## Independent (Unabhängig)

**Prinzip:** Stories sollten möglichst keine Abhängigkeiten voneinander haben.

**Problem:** Abhängigkeiten führen zu:
- Priorisierungsproblemen
- Erschwerter Schätzung

**Lösungsansätze:**
1. **Kombinieren:** Abhängige Stories zu einer größeren Story zusammenfassen
2. **Neu aufteilen:** Stories entlang einer anderen Dimension splitten
3. **Zwei Schätzungen:** Eine Schätzung für "davor", eine für "danach"

**Beispiel:**
- ❌ Schlecht: "Visa", "MasterCard", "Amex" als separate Stories
- ✅ Besser: "Ein Kunde kann mit einer Kreditkarte bezahlen" + "Ein Kunde kann mit zwei weiteren Kartentypen bezahlen"

---

## Negotiable (Verhandelbar)

**Prinzip:** Stories sind keine Verträge, sondern **Erinnerungen für Gespräche**.

**Story Card Struktur:**
- **Vorderseite:** Kurze Beschreibung + offene Fragen
- **Rückseite:** Test Cases

**Richtige Detailtiefe:**
- ✅ Gut: Genug Info zum Fortsetzen des Gesprächs
- ❌ Zu wenig: Keine Hinweise für spätere Diskussionen
- ❌ Zu viel: Wirkt wie finale Spezifikation, verhindert Konversation

**Beispiel guter Notes:**
```
Eine Firma kann für ein Jobangebot mit Kreditkarte bezahlen.
Note: Visa, MasterCard, American Express akzeptieren.
Discover Card in Betracht ziehen.
```

**Details werden zu Tests:**
- Test mit Visa, MasterCard, Amex (Pass)
- Test mit Diner's Club (Fail)
- Test mit abgelaufenen Karten
- Test über/unter $100

---

## Valuable (Wertvoll)

**Prinzip:** Stories müssen wertvoll sein für **Käufer ODER Nutzer** (nicht nur für Entwickler).

**Erlaubte Perspektiven:**
- Endnutzer (verwendet die Software)
- Käufer/Entscheider (kauft die Software)

**Zu vermeiden - Technologie-fokussiert:**
- ❌ "Alle DB-Verbindungen über Connection Pool"
- ❌ "Fehlerbehandlung über gemeinsame Klassen"

**Besser - Nutzen-orientiert:**
- ✅ "Bis zu 50 Nutzer können die App mit 5-User-DB-Lizenz verwenden"
- ✅ "Alle Fehler werden konsistent präsentiert und geloggt"

**Best Practice:** Kunde schreibt die Stories selbst

---

## Estimatable (Schätzbar)

**Gründe für nicht-schätzbare Stories:**

### 1. Fehlendes Domain-Wissen
- **Lösung:** Mit Kunden sprechen, Details klären

### 2. Fehlendes technisches Wissen
- **Lösung:** Spike (time-boxed Experiment)
- Story wird aufgeteilt in:
  - Investigative Story (Spike)
  - Funktionale Story

### 3. Story zu groß (Epic)
- **Lösung:** In kleinere Stories aufteilen

**Beispiel Spike:**
- "Untersuche Kreditkartenverarbeitung im Web" (timeboxed)
- "Ein Nutzer kann mit Kreditkarte bezahlen"

---

## Small (Klein)

**Prinzip:** Stories müssen "genau richtig" groß sein - nicht zu groß (Epic), nicht zu klein.

### Epics aufteilen

**Zwei Typen von Epics:**

1. **Compound Story** (zusammengesetzte Story)
   - Enthält mehrere kürzere Stories
   - Beispiel: "Nutzer kann Lebenslauf posten"

   **Split-Optionen:**
   - Entlang CRUD: Create, Edit, Delete, Activate/Deactivate
   - Entlang Datenkomponenten: Bildung, Berufserfahrung, Gehalt, etc.

2. **Complex Story** (komplexe Story)
   - Inherent groß durch Unsicherheit

   **Split in:**
   - Investigative Story (Spike, timeboxed)
   - Funktionale Story

### Zu kleine Stories kombinieren
- Bugs und UI-Änderungen oft zu klein
- **Lösung:** Gruppieren zu ~0.5-3 Tage Arbeit
- Beispiel: 5 Bugs + UI-Änderungen = 1 Story "Bug Fixes Iteration 3"

---

## Testable (Testbar)

**Prinzip:** Erfolgreich bestandene Tests beweisen, dass Story fertig ist.

**Nicht testbar - schlecht:**
- ❌ "Nutzer findet die Software einfach zu bedienen"
- ❌ "Nutzer muss nie lange auf Screens warten"

**Testbar - gut:**
- ✅ "Neue Screens erscheinen in 95% aller Fälle innerhalb 2 Sekunden"
- ✅ "Ein Anfänger kann häufige Workflows ohne Training abschließen" (beobachtbar durch UX-Test)

**Best Practices:**
- Strebe 99% Automatisierung an (nicht 10%)
- Vermeide "nie" - verwende "selten" mit messbaren Schwellwerten
- Definiere klare, messbare Kriterien

---

## Verantwortlichkeiten

### Entwickler
- Helfen beim Schreiben von Stories (Versprechen zu sprechen, nicht Spezifikationen)
- Sicherstellen: Wert, Unabhängigkeit, Testbarkeit, richtige Größe
- Technologie-Bedürfnisse in Nutzer-Wert übersetzen

### Kunde
- Schreiben von Stories mit den INVEST-Attributen
- Stories mit klarem Nutzer-/Käufer-Wert
- Bereitschaft zur Konversation über Details

---

## Praktische Tipps

2. **Bei Abhängigkeiten:** Erst kombinieren versuchen, dann neu splitten

3. **Bei Epics:** Als Platzhalter nutzen mit grober Schätzung, später aufteilen

4. **Spike timing:** Wenn möglich in separater Iteration vor funktionaler Story

5. **Details = Tests:** Zu viele Details auf Story Card vermeiden, stattdessen als Tests formulieren

---

## Quelle
Kapitel aus "User Stories Applied" von Mike Cohn - Grundlagentext zum INVEST-Prinzip
