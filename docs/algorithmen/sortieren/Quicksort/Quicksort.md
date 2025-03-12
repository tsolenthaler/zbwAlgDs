# Quicksort

Quicksort (englisch quick ‚schnell‘ und to sort ‚sortieren‘) ist ein schneller, rekursiver, nicht-stabiler Sortieralgorithmus, der nach dem Prinzip Teile und herrsche arbeitet. Er wurde ca. 1960 von C. Antony R. Hoare in seiner Grundform entwickelt und seitdem von vielen Forschern verbessert. Der Algorithmus hat den Vorteil, dass er über eine sehr kurze innere Schleife verfügt (was die Ausführungsgeschwindigkeit stark erhöht) und dass er, abgesehen von dem für die Rekursion zusätzlichen benötigten Platz auf dem Aufruf-Stack, ohne zusätzlichen Speicherplatz auskommt.

Im Durchschnitt führt der Quicksort-Algorithmus O ( n ⋅ log ⁡ ( n ) ) Vergleiche durch. Im schlechtesten Fall werden O ( n^2 ) Vergleiche durchgeführt, was aber in der Praxis sehr selten vorkommt.

## Prinzip von Quicksort

Zunächst wird die zu sortierende Liste in zwei Teillisten („linke“ und „rechte“ Teilliste) getrennt. Dazu wählt Quicksort ein sogenanntes Pivotelement aus der Liste aus. Alle Elemente, die kleiner als das Pivotelement sind, kommen in die linke Teilliste, und alle, die größer sind, in die rechte Teilliste. Die Elemente, die gleich dem Pivotelement sind, können sich beliebig auf die Teillisten verteilen. Nach der Aufteilung sind die Elemente der linken Liste kleiner oder gleich den Elementen der rechten Liste.

Anschließend muss man also noch jede Teilliste in sich sortieren, um die Sortierung zu vollenden. Dazu wird der Quicksort-Algorithmus jeweils auf der linken und auf der rechten Teilliste ausgeführt. Jede Teilliste wird dann wieder in zwei Teillisten aufgeteilt und auf diese jeweils wieder der Quicksort-Algorithmus angewandt, und so weiter. Diese Selbstaufrufe werden als Rekursion bezeichnet. Wenn eine Teilliste der Länge eins oder null auftritt, so ist diese bereits sortiert und es erfolgt der Abbruch der Rekursion.

Die Positionen der Elemente, die gleich dem Pivotelement sind, hängen vom verwendeten Teilungsalgorithmus ab. Sie können sich beliebig auf die Teillisten verteilen. Da sich die Reihenfolge von gleichwertigen Elementen zueinander ändern kann, ist Quicksort im Allgemeinen nicht stabil.

Das Verfahren muss sicherstellen, dass jede der Teillisten mindestens um eins kürzer ist als die Gesamtliste. Dann endet die Rekursion garantiert nach endlich vielen Schritten. Das kann z. B. dadurch erreicht werden, dass das ursprünglich als Pivot gewählte Element auf einen Platz zwischen den Teillisten gesetzt wird und somit zu keiner Teilliste gehört. 

## Pseudocode
Die Implementierung der Teilung erfolgt als In-place-Algorithmus: Die Elemente werden nicht in zusätzlichen Speicher kopiert, sondern nur innerhalb der Liste vertauscht. Dafür wird ein Verfahren verwendet, das als Teilen oder auch Partitionieren bezeichnet wird. Danach sind die beiden Teillisten gleich in der richtigen Position. Sobald die Teillisten in sich sortiert wurden, ist die Sortierung der Gesamtliste beendet.

Der folgende Pseudocode illustriert die Arbeitsweise des Algorithmus, wobei daten die zu sortierende Liste mit n Elementen ist. Bei jedem Aufruf von quicksort() gibt links den Index des ersten Elements in der Teilliste an und rechts den des letzten. Beim ersten Aufruf (oberste Rekursionsebene) ist links = 0 und rechts = n-1. Die übergebene Liste wird dabei rekursiv immer weiter geteilt, bis sie nur noch einen Wert enthält. 

```
funktion quicksort(links, rechts)
    falls links < rechts dann
        teiler:= teile(links, rechts)
        quicksort(links, teiler - 1)
        quicksort(teiler + 1, rechts)
    ende
ende
```
Die folgende Implementierung der Funktion teile teilt das Feld so, dass sich das Pivotelement an seiner endgültigen Position befindet und alle kleineren Elemente davor stehen, während alle größeren danach kommen: 

```
funktion teile(links, rechts)
     i:= links
     // Starte mit j links vom Pivotelement
     j:= rechts - 1
     pivot:= daten[rechts]

     wiederhole solange i < j // solange i an j nicht vorbeigelaufen ist
         // Suche von links ein Element, welches größer als das Pivotelement ist
         wiederhole solange i < j und daten[i] <= pivot
             i:= i + 1
         ende

         // Suche von rechts ein Element, welches kleiner oder gleich dem Pivotelement ist
         wiederhole solange j > i und daten[j] > pivot
             j:= j - 1
         ende

         falls daten[i] > daten[j] dann
             tausche daten[i] mit daten[j]
         ende
     ende

     // Tausche Pivotelement (daten[rechts]) mit neuer endgültiger Position (daten[i])
     // und gib die neue Position des Pivotelements zurück, beende Durchlauf
     falls daten[i] > pivot dann
         tausche daten[i] mit daten[rechts]
     sonst
         i:= rechts
     ende
     antworte i
 ende
```

## Vorteile

* Hohe Geschwindigkeit: Quicksort hat im Durchschnitt eine Zeitkomplexität von O(n log n), was ihn zu einem der schnellsten Sortieralgorithmen macht. Die innere Schleife ist sehr kurz, was die Ausführungsgeschwindigkeit erhöht.
* In-Place-Sortierung: Quicksort benötigt keinen zusätzlichen Speicherplatz für die Sortierung, abgesehen von dem Platz, der für die Rekursion auf dem Aufruf-Stack benötigt wird. Dies macht ihn speichereffizient.
* Einfachheit der Implementierung: Der Algorithmus ist relativ einfach zu implementieren und wird in vielen Standardbibliotheken verwendet.
* Gute Leistung in der Praxis: Die zufällige Wahl des Pivotelements im iterativen Ansatz verringert die Wahrscheinlichkeit, in den Worst Case zu geraten, und sorgt für eine bessere durchschnittliche Leistung.
* Reduzierung der Rekursionstiefe: Der iterative Ansatz kann die Rekursionstiefe verringern und somit den Speicherbedarf reduzieren, da der Stapelspeicher mit hoher Wahrscheinlichkeit kleiner als 2·log2(n) ist.
* Kombination mit Insertionsort: Die Möglichkeit, bei kleinen Teillisten auf Insertionsort umzuschalten, kann die Effizienz weiter steigern, da Insertionsort für kleine Datenmengen sehr schnell ist.

## Nachteile

* Schlechtester Fall: Im schlechtesten Fall, wenn das Pivotelement ungünstig gewählt wird (z. B. immer das größte oder kleinste Element), kann die Zeitkomplexität auf O(n²) ansteigen. Dies kann bei bereits sortierten oder fast sortierten Daten der Fall sein.
* Nicht stabil: Quicksort ist ein nicht-stabiler Sortieralgorithmus, was bedeutet, dass die relative Reihenfolge von gleichwertigen Elementen nicht garantiert bleibt.
* Komplexität der Implementierung bei Optimierungen: Obwohl der iterative Ansatz einige Vorteile bietet, kann die Implementierung komplexer werden, insbesondere wenn zusätzliche Optimierungen wie die Wahl eines geeigneten Pivotelements oder der Wechsel zu Insertionsort berücksichtigt werden müssen.
* Effizienz bei kleinen Listen: Quicksort kann ineffizient werden, wenn die zu sortierende Liste sehr klein ist, da die Anzahl der Vergleiche und Vertauschungen in solchen Fällen relativ hoch sein kann. Der Wechsel zu Insertionsort kann dies jedoch mildern.
* Möglicher Stapelüberlauf: Obwohl der iterative Ansatz den Speicherbedarf verringert, besteht immer noch das Risiko eines Stapelüberlaufs, wenn die Liste sehr groß ist und die Rekursionstiefe nicht ausreichend kontrolliert wird.

## Anwendung

### Geeignete Einsatzbereiche:

* Große Datenmengen: Quicksort ist besonders effektiv bei der Sortierung großer Datenmengen, da er im Durchschnitt eine Zeitkomplexität von O(n log n) aufweist.

* In-Memory-Sortierung: Quicksort eignet sich gut für die Sortierung von Daten, die im Arbeitsspeicher (RAM) gehalten werden können, da er ein In-Place-Verfahren ist und keinen zusätzlichen Speicherplatz benötigt (außer für den Rekursions-Stack).

* Dynamische Daten: In Anwendungen, in denen Daten häufig hinzugefügt oder entfernt werden, kann Quicksort schnell auf neue Daten reagieren, insbesondere wenn die Daten nicht bereits sortiert sind.

* Echtzeitanwendungen: Aufgrund seiner Geschwindigkeit ist Quicksort in Echtzeitanwendungen nützlich, in denen schnelle Sortierungen erforderlich sind, wie z. B. in der Spieleentwicklung oder bei der Verarbeitung von Streaming-Daten.

### Abgrenzungen und weniger geeignete Einsatzbereiche:

* Kleine Datenmengen: Bei sehr kleinen Datenmengen kann Quicksort ineffizient sein, da die Overhead-Kosten der Rekursion und der Partitionierung im Vergleich zu einfacheren Algorithmen wie Insertionsort überwiegen. In solchen Fällen kann es sinnvoll sein, auf Insertionsort oder andere einfache Sortieralgorithmen umzuschalten.

*  Stabilität: Quicksort ist ein nicht-stabiler Sortieralgorithmus, was bedeutet, dass die relative Reihenfolge von gleichwertigen Elementen nicht garantiert bleibt. In Anwendungen, in denen die Stabilität wichtig ist (z. B. bei der Sortierung von Datensätzen mit mehreren Schlüsseln), könnte ein stabiler Algorithmus wie Mergesort die bessere Wahl sein.

* Worst-Case-Szenarien: In Fällen, in denen die Daten bereits sortiert oder fast sortiert sind, kann Quicksort in den Worst Case (O(n²)) fallen, wenn das Pivotelement ungünstig gewählt wird. In solchen Szenarien sind Algorithmen wie Heapsort oder Mergesort, die eine garantierte O(n log n) Laufzeit haben, möglicherweise besser geeignet.

* Begrenzter Speicher: Obwohl Quicksort speichereffizient ist, kann die Rekursionstiefe in extremen Fällen zu einem Stapelüberlauf führen. In Umgebungen mit stark begrenztem Speicher könnte dies ein Problem darstellen.

* Parallelisierung: Quicksort kann schwieriger zu parallelisieren sein als andere Algorithmen wie Mergesort, die sich besser für parallele Verarbeitung eignen. In Anwendungen, die von Parallelität profitieren, könnte Mergesort die bessere Wahl sein.

## Implementierung

```C#
using System;

class Program
{
    static void Main(string[] args)
    {
        int[] daten = { 9, 7, 5, 11, 12, 2, 14, 3, 10, 6 };
        int rechts = daten.Length - 1;
        int pivotIndex = Teile(daten, 0, rechts);
        
        Console.WriteLine("Pivot-Index: " + pivotIndex);
        Console.WriteLine("Partitioniertes Array: " + string.Join(", ", daten));
    }

    static int Teile(int[] daten, int links, int rechts)
    {
        int i = links;
        int j = rechts - 1;
        int pivot = daten[rechts];

        while (i < j) // solange i an j nicht vorbeigelaufen ist
        {
            // Suche von links ein Element, welches größer als das Pivotelement ist
            while (i < j && daten[i] <= pivot)
            {
                i++;
            }

            // Suche von rechts ein Element, welches kleiner oder gleich dem Pivotelement ist
            while (j > i && daten[j] > pivot)
            {
                j--;
            }

            // Tausche daten[i] mit daten[j], wenn nötig
            if (daten[i] > daten[j])
            {
                Tausche(daten, i, j);
            }
        }

        // Tausche Pivotelement (daten[rechts]) mit neuer endgültiger Position (daten[i])
        if (daten[i] > pivot)
        {
            Tausche(daten, i, rechts);
        }
        else
        {
            i = rechts;
        }

        return i; // Rückgabe der neuen Position des Pivotelements
    }

    static void Tausche(int[] daten, int index1, int index2)
    {
        int temp = daten[index1];
        daten[index1] = daten[index2];
        daten[index2] = temp;
    }
}
```

## Links

* [https://de.wikipedia.org/wiki/Quicksort](https://de.wikipedia.org/wiki/Quicksort)
* [https://studyflix.de/informatik/quicksort-1322](https://studyflix.de/informatik/quicksort-1322)
* [Wikibooks](https://de.wikibooks.org/wiki/Algorithmensammlung:_Sortierverfahren:_Quicksort#C#)