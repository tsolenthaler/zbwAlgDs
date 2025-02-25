# Binary Tree Sort

## Vor- und Nachteile
Der Algorithmus wird üblicherweise anhand einer existierenden Implementierung zur Verwaltung und Manipulation von binären Bäumen implementiert. Auf dieser Grundlage kann er auf zwei einfache Arbeitsschritte – das Anlegen des Baumes und den in-order-Durchlauf – reduziert werden und damit sehr schnell umgesetzt werden.

Gegen ihn spricht die hohe Zeitkomplexität im Worst Case, der große Aufwand für die einzelnen Operationen, der zusätzliche Speicherbedarf sowie die im Verhältnis zu seiner Effizienz aufwendige Implementierung, falls diese von Grund auf neu erfolgen muss.

Stellt die genannte existierende Implementierung allerdings balancierte Suchbäume zur Verfügung, fällt ein Großteil dieser Nachteile weg.

Ähnlich wie Bubblesort wird Binary Tree Sort kaum bei realen Problemen eingesetzt. 