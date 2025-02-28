# Shellsort

* Instabil
* In-Place
* Basiert auf den Insertionsort

* Listengrösse (Anzahl der Elemente) wird defineirt
    * Bspw. 4, 2, 1 für die Iterationen

* Komplexität
    * O(n^2)

## Vorteile

* Effiziente Vorab-Sortierung: Durch die Aufteilung der unsortierten Folge in Teilfolgen und die schrittweise Sortierung mit abnehmenden Abständen wird eine grobe Sortierung erreicht, die die nachfolgenden Sortierschritte erleichtert.

* In-Place-Sortierung: Shellsort benötigt nur einen minimalen zusätzlichen Speicherplatz, da die Sortierung direkt im Originalarray erfolgt.

* Reduzierte Verschiebungen: Im Vergleich zu einem normalen Insertionsort müssen die Elemente nicht so weit verschoben werden, was die Effizienz bei der Sortierung verbessert.

* Flexibilität bei der Gap-Sequenz: Die Möglichkeit, verschiedene Gap-Sequenzen zu verwenden, ermöglicht eine Anpassung an spezifische Datensätze, was die Leistung optimieren kann.

* Einfachheit der Implementierung: Die Implementierung von Shellsort ist relativ unkompliziert und erfordert nicht viel Code.

## Nachteile

* Nicht stabil: Shellsort ist kein stabiler Sortieralgorithmus. Die Sortierung über Distanz kann dazu führen, dass benachbarte Elemente in der Reihenfolge vertauscht werden.

* Schlechtere Worst-Case-Leistung: Im schlimmsten Fall kann die Laufzeit von Shellsort O(n^2) betragen, was im Vergleich zu effizienteren Algorithmen wie Quicksort oder Mergesort ungünstig ist.

* Abhängigkeit von der Gap-Sequenz: Die Wahl der Gap-Sequenz hat einen erheblichen Einfluss auf die Leistung. Eine suboptimale Wahl kann die Effizienz stark beeinträchtigen.

* Komplexität der Analyse: Die Analyse der Laufzeit von Shellsort ist komplex und variiert je nach gewählter Gap-Sequenz, was es schwierig macht, eine allgemeine Aussage über die Leistung zu treffen.

* Praktische Ineffizienz der ursprünglichen Gap-Sequenz: Die von Shell ursprünglich vorgeschlagene Schrittfolge (1, 2, 4, 8, 16, ...) hat sich in der Praxis als nicht optimal erwiesen, da sie nur gerade Stellen sortiert und ungerade Stellen erst im letzten Schritt behandelt.


## Anwendung

## Implementierung

## Links

* [Wikipedia](https://de.wikipedia.org/wiki/Shellsort)
* [https://studyflix.de/informatik/shellsort-1411](https://studyflix.de/informatik/shellsort-1411)