# Shellsort

* Instabil
* In-Place
* Basiert auf den Insertionsort

* Listengrösse (Anzahl der Elemente) wird defineirt
    * Bspw. 4, 2, 1 für die Iterationen

* Komplexität
    * O(n^2)

## Beschreibung
Shellsort ist ein von Donald L. Shell im Jahr 1959 entwickeltes Sortierverfahren, das auf dem Sortierverfahren des direkten Einfügens (Insertionsort) basiert. 

## Prinzip
Der Grundgedanke besteht darin, die unsortierte Folge so umzuordnen, dass man eine sortierte Teilfolge enthält, wenn man jedes h-te Element entnimmt. Das soll für jedes beliebige Anfangsfeld gelten.[1]

Der Algorithmus von Shellsort setzt diese Idee um, indem er die unsortierte Folge in mehrere Teilfolgen aufteilt und danach die Einträge innerhalb jeder Teilfolge sortiert. Beispielsweise führt eine Aufteilung in 4 Teilfolgen zu einer Teilfolge mit den Indizes 0, 4, 8, … einer anderen mit den Indizes 1, 5, 9, … und so weiter. Nach einem solchen Sortierschritt nennt man die Folge 4-sortiert.

Shellsort wiederholt mehrere Sortierschritte. Der erste Sortierschritt erzeugt die meisten Teilfolgen, also auch den größten Abstand zwischen den Indizes einer Teilfolge. Der Abstand wird mit jedem Schritt kleiner. Wenn z. B. Shellsort mit Abstand 4 anfängt, dann wird die Folge erst 4-sortiert, dann 2-sortiert, und zuletzt mit normalem Insertionsort sozusagen 1-sortiert.

Anschaulich wäre dies anhand von Hilfsmatrizen darzustellen (siehe Beispiel):

* Die Daten werden in eine k-spaltige Matrix zeilenweise geschrieben
* Die Spalten der Matrix werden einzeln sortiert

Daraus resultiert eine grobe Sortierung. Dieser Schritt wird mehrmals wiederholt, wobei jeweils die Breite der Matrix verringert wird, bis die Matrix nur noch aus einer einzigen vollständig sortierten Spalte besteht.

Eine a*b-sortierte Sequenz ist nicht auch automatisch a-sortiert oder b-sortiert. Zum Beweis betrachten wir eine Sequenz aus den Zahlen 1 bis 12. Diese ist 6-sortiert, wenn wir auf eine beliebige Permutation der Zahlen 1, 2, 3, 4, 5, 6 eine ebenfalls beliebige Permutation der Zahlen 7, 8, 8, 10, 11, 12 folgen lassen. Die Permutation 6, 5, 4, 3, 2, 1 ist aber keinesfalls 2- oder 3-sortiert. 6, 5, 4, 3, 2, 1, 7, 8, 9, 10, 11, 12 ist 6-sortiert, aber nicht 2- und auch nicht 3-sortiert.

Shellsort arbeitet in-place, gehört jedoch nicht zu den stabilen Sortieralgorithmen. Aufgrund der Sortierung über Distanz verliert die Sortiermethode ihre Eigenschaft „stabil“. Zwei benachbarte und sortierte Elemente landen in verschiedenen Untersequenzen und werden möglicherweise so umsortiert, dass ihre Reihenfolge vertauscht wird. 


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

## Einsatzbereiche von Shellsort:

* Kleine bis mittelgroße Datensätze: Shellsort eignet sich gut für die Sortierung von kleinen bis mittelgroßen Datenmengen, da die Implementierung einfach ist und der Algorithmus in der Regel schneller als einfachere Sortieralgorithmen wie Insertion Sort oder Bubble Sort arbeitet.

* Fast sortierte Daten: Der Algorithmus zeigt eine besonders gute Leistung, wenn die Daten bereits teilweise sortiert sind. In solchen Fällen kann die Laufzeit erheblich reduziert werden.

* In-Place-Sortierung: Da Shellsort in-place arbeitet und nur einen minimalen zusätzlichen Speicher benötigt, ist er nützlich in Umgebungen, in denen der Speicher begrenzt ist.

* Einfache Implementierung: Aufgrund der relativ einfachen Implementierung kann Shellsort in Anwendungen eingesetzt werden, in denen eine schnelle und unkomplizierte Sortierlösung benötigt wird.

## Abgrenzung von Shellsort:

* Nicht stabil: Shellsort ist kein stabiler Sortieralgorithmus, was bedeutet, dass die relative Reihenfolge von gleichen Elementen nicht garantiert ist. Dies kann in Anwendungen problematisch sein, in denen die Stabilität der Sortierung wichtig ist.

* Schlechtere Worst-Case-Leistung: Im Vergleich zu effizienteren Algorithmen wie Quicksort oder Mergesort hat Shellsort im schlimmsten Fall eine Laufzeit von O(n^2). Daher ist er nicht die beste Wahl für sehr große Datensätze oder in Situationen, in denen die Leistung entscheidend ist.

* Abhängigkeit von der Gap-Sequenz: Die Leistung von Shellsort hängt stark von der Wahl der Gap-Sequenz ab. Eine suboptimale Wahl kann die Effizienz des Algorithmus erheblich beeinträchtigen, was ihn weniger flexibel macht als einige andere Sortieralgorithmen.

* Einsatz in speziellen Anwendungen: Shellsort wird oft in speziellen Anwendungen eingesetzt, wo die oben genannten Einschränkungen akzeptabel sind, und wo die Vorteile der In-Place-Sortierung und der einfachen Implementierung überwiegen

## Implementierung

```C#
using System;

class Program
{
    static void Shellsort(int[] a, int n)
    {
        int i, j, k, h, t;

        // Gap-Sequenz
        int[] spalten = { 2147483647, 1131376761, 410151271, 157840433,
                          58548857, 21521774, 8810089, 3501671, 
                          1355339, 543749, 213331, 84801, 
                          27901, 11969, 4711, 1968, 815, 
                          271, 111, 41, 13, 4, 1 };

        for (k = 0; k < spalten.Length; k++)
        {
            h = spalten[k];
            // Sortiere die "Spalten" mit Insertionsort
            for (i = h; i < n; i++)
            {
                t = a[i];
                j = i;
                while (j >= h && a[j - h] > t)
                {
                    a[j] = a[j - h];
                    j = j - h;
                }
                a[j] = t;
            }
        }
    }

    static void Main(string[] args)
    {
        int[] array = { 5, 2, 9, 1, 5, 6 };
        int n = array.Length;

        Console.WriteLine("Unsortiertes Array:");
        Console.WriteLine(string.Join(", ", array));

        Shellsort(array, n);

        Console.WriteLine("Sortiertes Array:");
        Console.WriteLine(string.Join(", ", array));
    }
}
```

## Links

* [Wikipedia](https://de.wikipedia.org/wiki/Shellsort)
* [https://studyflix.de/informatik/shellsort-1411](https://studyflix.de/informatik/shellsort-1411)