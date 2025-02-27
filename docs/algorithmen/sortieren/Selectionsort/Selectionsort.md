# Selectionsort

* einfach
* instabil
* "Sortieren nach direktes Auswählen"
    * kleinste oder grösste Element
        * minSort
        * maxSort
* Keine Unterschiede im Best Case oder Worst Case


Formel der Anzahl Vergleiche = n (n-1)/2

## Vorteile

* Einfachheit: Selection Sort ist leicht zu verstehen und zu implementieren, was ihn zu einem guten Lehrwerkzeug für grundlegende Sortierkonzepte macht.
* In-Place-Sortierung: Der Algorithmus benötigt nur eine konstante Menge an zusätzlichem Speicher (O(1)), da die Sortierung direkt im ursprünglichen Array erfolgt.
* Flexibilität: Der Algorithmus kann leicht angepasst werden, um entweder aufsteigend oder absteigend zu sortieren, indem man entweder das kleinste oder das größte Element auswählt.
* Stabilität: Obwohl der Standard-Selection Sort instabil ist, kann er so implementiert werden, dass er stabil ist, was bedeutet, dass die Reihenfolge gleichwertiger Elemente erhalten bleibt.

## Nachteile

* Ineffizienz: Die Zeitkomplexität von O(n²) macht den Algorithmus für große Datensätze ineffizient, da die Anzahl der Vergleiche und Tauschoperationen mit der Größe des Arrays quadratisch ansteigt.
* Langsame Leistung: Im Vergleich zu effizienteren Sortieralgorithmen wie Quicksort oder Mergesort ist Selection Sort in der Regel langsamer, insbesondere bei größeren Listen.
* Wenig Anpassungsfähigkeit: Der Algorithmus ist nicht adaptiv, was bedeutet, dass er nicht erkennt, wenn die Liste bereits teilweise sortiert ist, und dennoch die gleichen Schritte ausführt.
* Hohe Anzahl an Vergleichen: Selbst im besten Fall benötigt der Algorithmus eine große Anzahl an Vergleichen (n * (n - 1) / 2), was seine Effizienz weiter einschränkt.


## Anwendungen

### Einsatzbereiche:

* Lehrzwecke: Aufgrund seiner Einfachheit und der klaren Struktur eignet sich Selection Sort hervorragend als Einführung in Sortieralgorithmen in der Informatik-Ausbildung.
* Kleine Datensätze: Bei sehr kleinen Arrays oder Listen kann Selection Sort aufgrund des geringen Overheads und der einfachen Implementierung eine akzeptable Leistung bieten.
* Eingeschränkte Ressourcen: In Umgebungen mit sehr begrenztem Speicher (z. B. eingebettete Systeme) kann Selection Sort vorteilhaft sein, da er in-place arbeitet und nur eine konstante Menge an zusätzlichem Speicher benötigt.
* Stabilität: Wenn eine stabile Sortierung erforderlich ist und die Liste klein ist, kann eine angepasste Version von Selection Sort verwendet werden.

### Abgrenzung

* Vergleich mit anderen Sortieralgorithmen: Im Vergleich zu effizienteren Algorithmen wie Quicksort, Mergesort oder Heapsort ist Selection Sort in der Regel langsamer, insbesondere bei größeren Datensätzen. Diese Algorithmen haben eine bessere durchschnittliche und worst-case Zeitkomplexität (O(n log n)).
* Nicht adaptiv: Selection Sort ist nicht adaptiv, was bedeutet, dass er nicht von bereits sortierten oder teilweise sortierten Daten profitiert. Algorithmen wie Insertion Sort sind in solchen Fällen effizienter.
* Instabilität: In seiner Standardform ist Selection Sort instabil, was bedeutet, dass die relative Reihenfolge gleichwertiger Elemente nicht garantiert ist. Für Anwendungen, bei denen die Stabilität wichtig ist, sind andere Algorithmen wie Mergesort oder eine angepasste Version von Insertion Sort besser geeignet.
* Einsatz in der Praxis: In der Praxis wird Selection Sort selten verwendet, da es in den meisten realen Anwendungen effizientere Alternativen gibt. Er wird hauptsächlich in speziellen Fällen oder zu Bildungszwecken eingesetzt.


## Implementierung

```C#
static void SelectionSort(ref List<int> feld)
{
    // alle Zahlen durchlaufen
    for (int i = 0; i < feld.Count; i++)
    {
        // Position min der kleinsten Zahl ab Position i suchen
        int min = i;
        for (int j = i + 1; j < feld.Count; j++)
        {
            if (feld[j] < feld[min])
            {    
              min = j;
            }
        }
        // Zahl an Position i mit der kleinsten Zahl vertauschen
        int tmp = feld[min];
        feld[min] = feld[i];
        feld[i] = tmp;
    }
}
```

## Links

* [Wikiepdia Selectionsort](https://de.wikipedia.org/wiki/Selectionsort)
* [https://studyflix.de/informatik/selectionsort-1323](https://studyflix.de/informatik/selectionsort-1323)
* [Wikibooks](https://de.wikibooks.org/wiki/Algorithmensammlung:_Sortierverfahren:_Selectionsort)