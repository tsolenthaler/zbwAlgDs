# Binary Tree Sort

## Prinzip

Bei diesem Algorithmus werden alle zu sortierenden Elemente nacheinander in einen binären Suchbaum eingefügt. Anschließend wird dieser Baum in-order durchlaufen, wobei alle Elemente in sortierter Reihenfolge angetroffen werden.

In seiner ganz elementaren Form ist der Algorithmus nicht stabil. Wird jedoch statt der üblichsten Suchfunktion Find eine Variante genommen, die auch bei vorhandenem Schlüssel entweder rechts- oder linksseitig immer bis zu den Blättern hinab sucht, wird der Sortieralgorithmus stabil. Dies kann mittels einer Vergleichsfunktion geschehen, die bei Gleichheit statt dem Rückgabewert 0 immer nur den Wert +1 oder immer nur den Wert −1 zurückgibt (bei gleicher Suchfunktion) resp. einer angepassten Suchfunktion, wie z. B. FindDupGE. 

## Komplexität

Die durchschnittliche Komplexität beträgt O ( n log ⁡ n ), im Worst Case einer bereits sortierten Liste ist sie jedoch Θ ( n 2 ). Wird statt des unbalancierten ein balancierter binärer Suchbaum genommen, ist die Komplexität auch im Worst Case O ( n log ⁡ n ).

Für den aufzubauenden Suchbaum wird O ( n ) zusätzlicher Speicher benötigt. 

## Vorteile

* Einfache Implementierung: Der Algorithmus kann auf zwei einfache Arbeitsschritte reduziert werden – das Anlegen des Baumes und den In-Order-Durchlauf – was eine schnelle Umsetzung ermöglicht.
* Nutzung existierender Implementierungen: Wenn balancierte Suchbäume zur Verfügung stehen, können viele der Nachteile des Binary Tree Sort vermieden werden.

## Nachteile

* Hohe Zeitkomplexität im Worst Case: Im schlimmsten Fall kann die Zeitkomplexität ineffizient sein.
* Großer Aufwand für Operationen: Die einzelnen Operationen können aufwendig sein, insbesondere bei unbalancierten Bäumen.
* Zusätzlicher Speicherbedarf: Jeder Knoten benötigt zusätzlichen Speicher für Zeiger auf die Kindknoten.
* Aufwendige Implementierung: Wenn der Algorithmus von Grund auf neu implementiert werden muss, kann dies im Verhältnis zu seiner Effizienz aufwendig sein.
* Seltene Anwendung in der Praxis: Ähnlich wie Bubblesort wird Binary Tree Sort kaum bei realen Problemen eingesetzt.


### Zusammenfassung
Der Algorithmus wird üblicherweise anhand einer existierenden Implementierung zur Verwaltung und Manipulation von binären Bäumen implementiert. Auf dieser Grundlage kann er auf zwei einfache Arbeitsschritte – das Anlegen des Baumes und den in-order-Durchlauf – reduziert werden und damit sehr schnell umgesetzt werden.

Gegen ihn spricht die hohe Zeitkomplexität im Worst Case, der große Aufwand für die einzelnen Operationen, der zusätzliche Speicherbedarf sowie die im Verhältnis zu seiner Effizienz aufwendige Implementierung, falls diese von Grund auf neu erfolgen muss.

Stellt die genannte existierende Implementierung allerdings balancierte Suchbäume zur Verfügung, fällt ein Großteil dieser Nachteile weg.

Ähnlich wie Bubblesort wird Binary Tree Sort kaum bei realen Problemen eingesetzt. 


### Links

* [https://de.wikipedia.org/wiki/Binary_Tree_Sort](https://de.wikipedia.org/wiki/Binary_Tree_Sort)