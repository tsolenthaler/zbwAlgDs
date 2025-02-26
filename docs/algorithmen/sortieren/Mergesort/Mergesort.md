# Mergesort

## Vorteile

* Stabile Sortierung: Mergesort ist ein stabiler Sortieralgorithmus, was bedeutet, dass die relative Reihenfolge von gleichen Elementen beibehalten wird. Dies ist besonders wichtig in Anwendungen, bei denen die Stabilität der Sortierung erforderlich ist.

* Effiziente Zeitkomplexität: Die Zeitkomplexität von Mergesort beträgt O(n log n) in allen Fällen (Worst-, Best- und Average-Case). Dies macht ihn hinsichtlich der Komplexität Quicksort überlegen, insbesondere da Quicksort im Worst-Case eine Komplexität von Θ(n²) aufweist.

* Geeignet für große Datenmengen: Mergesort kann effizient mit großen Datenmengen umgehen, da er auch auf externen Speichermedien gut funktioniert. Dies ist besonders vorteilhaft, wenn die Daten nicht vollständig im Hauptspeicher gehalten werden können.

* Rekursive Struktur: Die rekursive Natur von Mergesort ermöglicht eine klare und elegante Implementierung, die leicht zu verstehen ist. Die Aufteilung der Daten in kleinere Teillisten und deren anschließende Zusammenführung ist intuitiv.

* Korrektheit und Terminierung: Der Rekursionsabbruch stellt sicher, dass der Algorithmus terminieren kann, und die Korrektheit wird durch die strukturierte Zusammenführung der sortierten Teillisten gewährleistet.

## Nachteile

* Zusätzlicher Speicherbedarf: Mergesort benötigt zusätzlichen Speicherplatz, um die temporären Arrays für die Zusammenführung zu speichern, was O(n) an zusätzlichem Speicher erfordert. Dies kann bei großen Datenmengen problematisch sein, da es nicht als In-place-Verfahren gilt.

* Langsame Ausführung für kleine Datensätze: Für kleine Datensätze kann Mergesort langsamer sein als einfachere Algorithmen wie Insertion Sort oder Selection Sort, da der Overhead für das Teilen und Zusammenführen nicht gerechtfertigt ist.

* Komplexität der Implementierung: Obwohl die rekursive Struktur von Mergesort klar ist, kann die Implementierung des Merge-Schrittes komplex sein, insbesondere wenn man die Stabilität und Effizienz im Auge behalten möchte.

* Nicht in-place bei Arrays: Mergesort arbeitet in der Regel nicht in-place bei Arrays, was bedeutet, dass zusätzliche Datenstrukturen benötigt werden, um die Sortierung durchzuführen. Dies kann die Effizienz in Bezug auf den Speicherverbrauch beeinträchtigen.

## Anwendung

## Impelementierung

## Links

* [https://de.wikipedia.org/wiki/Mergesort](https://de.wikipedia.org/wiki/Mergesort)
* [https://studyflix.de/informatik/mergesort-1324](https://studyflix.de/informatik/mergesort-1324)