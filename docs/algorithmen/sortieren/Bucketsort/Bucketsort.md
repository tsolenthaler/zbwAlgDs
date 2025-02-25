# Bucketsort

Bucketsort (von englisch bucket „Eimer“) ist ein Sortierverfahren, das für bestimmte Werte-Verteilungen eine Eingabe-Liste in linearer Zeit sortiert. Der Algorithmus ist in drei Phasen eingeteilt:

    Verteilung der Elemente auf die Buckets (Partitionierung)
    Jeder Bucket wird mit einem weiteren Sortierverfahren wie beispielsweise Mergesort sortiert.
    Der Inhalt der sortierten Buckets wird konkateniert.

Das Verfahren arbeitet also out-of-place. 

## Vorteile

* Lineare Laufzeit: Bei gleichmäßiger Verteilung der Elemente kann Bucketsort in linearer Zeit (O(n)) arbeiten.
* Stabilität: Der Algorithmus kann stabil sortieren, wenn ein stabiler Sortieralgorithmus (wie Mergesort) für die Sortierung der Buckets verwendet wird.
* Effiziente Verarbeitung: Bei bestimmten Verteilungen, bei denen die Summe der Elemente in den Buckets asymptotisch linear ist, bleibt die Laufzeit ebenfalls in O(n).
*  Flexibilität: Bucketsort kann mit verschiedenen Sortieralgorithmen für die Buckets kombiniert werden, was Anpassungen an spezifische Anforderungen ermöglicht.
* Geringer Speicherbedarf: Der Speicherbedarf liegt in O(n), was für große Datenmengen vorteilhaft ist.

## Nachteile:

* Abhängigkeit von der Verteilung: Die Effizienz des Algorithmus hängt stark von der Verteilung der Eingabewerte ab; bei ungünstigen Verteilungen kann die Laufzeit erheblich steigen.
* Worst-Case-Szenario: Wenn alle Elemente in einen einzigen Bucket fallen, kann die Laufzeit auf O(n log n) ansteigen, was die Vorteile der linearen Laufzeit zunichte macht.
* Out-of-Place: Bucketsort arbeitet out-of-place, was bedeutet, dass zusätzlicher Speicher benötigt wird, um die Buckets zu speichern.
* Komplexität der Implementierung: Die Implementierung kann komplexer sein als bei anderen Sortieralgorithmen, insbesondere wenn mehrere Sortierstufen (Sub-Buckets) erforderlich sind.
* Eingeschränkte Anwendbarkeit: Bucketsort ist am effektivsten für Daten, die in einem bestimmten Intervall liegen und gleichmäßig verteilt sind, was seine Anwendbarkeit einschränken kann.

## Anwendung?

## Impelementierung?

## Links

* [https://de.wikipedia.org/wiki/Bucketsort](https://de.wikipedia.org/wiki/Bucketsort)