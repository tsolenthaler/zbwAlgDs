# Shellsort

* Instabil
* In-Place
* Basiert auf den Insertionsort

* Listengrösse (Anzahl der Elemente) wird defineirt
    * Bspw. 4, 2, 1 für die Iterationen

* Komplexität
    * O(n^2)

## Vorteile

* Effizienz bei großen Datenmengen: Shellsort kann in vielen Fällen schneller sein als einfache Sortieralgorithmen wie Insertion Sort oder Bubble Sort, insbesondere bei größeren Datensätzen.

* In-Place-Sortierung: Der Algorithmus benötigt nur eine geringe Menge an zusätzlichem Speicher, da er die Elemente im Originalarray sortiert.

* Einfach zu implementieren: Die Implementierung von Shellsort ist relativ einfach und erfordert nicht viel Code.

* Flexibilität bei der Wahl der Abstände: Die Wahl der "Gap"-Sequenz (Abstände zwischen den verglichenen Elementen) kann angepasst werden, um die Leistung zu optimieren. Verschiedene Sequenzen können unterschiedliche Laufzeiten ergeben.

* Stabilität: Shellsort kann stabil implementiert werden, was bedeutet, dass die relative Reihenfolge von gleichen Elementen beibehalten werden kann.

## Nachteile

* Schlechtere Worst-Case-Leistung: Im schlimmsten Fall kann die Laufzeit von Shellsort O(n^2) betragen, was schlechter ist als bei anderen effizienteren Algorithmen wie Quicksort oder Mergesort.

* Abhängigkeit von der Gap-Sequenz: Die Wahl der Gap-Sequenz hat einen großen Einfluss auf die Leistung. Eine suboptimale Wahl kann die Effizienz erheblich beeinträchtigen.

* Nicht stabil: In der Standardimplementierung ist Shellsort nicht stabil, was bedeutet, dass die relative Reihenfolge von gleichen Elementen nicht garantiert ist.

* Schwierigkeiten bei der Analyse: Die Analyse der Laufzeit von Shellsort ist komplex und hängt stark von der gewählten Gap-Sequenz ab, was es schwierig macht, eine allgemeine Aussage über die Leistung zu treffen.

## Anwendung

## Implementierung

## Links

* [Wikipedia](https://de.wikipedia.org/wiki/Shellsort)
* [https://studyflix.de/informatik/shellsort-1411](https://studyflix.de/informatik/shellsort-1411)