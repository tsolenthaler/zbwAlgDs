# Heapsort

## Vorteile:

* Asymptotisch optimale Komplexität: Heapsort hat eine Zeitkomplexität von O(n log n), was es asymptotisch optimal für Sortieralgorithmen macht, die auf Vergleichen basieren.
* In-Place-Sortierung: Der Algorithmus benötigt keinen zusätzlichen Speicherplatz für die Sortierung, da er in-place arbeitet. Dies bedeutet, dass die Sortierung direkt im ursprünglichen Array erfolgt.
* Worst-Case-Garantie: Heapsort hat eine garantierte Worst-Case-Laufzeit von O(n log n), was ihn in Szenarien mit vorsortierten Daten vorteilhaft macht, im Gegensatz zu anderen Algorithmen wie Quicksort, die im Worst Case O(n²) benötigen.
* Stabilität bei großen Datenmengen: Die Bottom-Up-Variante von Heapsort kann in bestimmten Fällen effizienter sein, insbesondere wenn die Vergleichsoperationen teuer sind.

## Nachteile:

* Instabilität: Heapsort ist nicht stabil, was bedeutet, dass die relative Reihenfolge von gleichen Elementen nicht garantiert bleibt. Dies kann in bestimmten Anwendungen problematisch sein.
* Langsame konstante Faktoren: In der Praxis ist Heapsort oft langsamer als andere Sortieralgorithmen wie Quicksort oder Introsort, insbesondere bei unsortierten oder teilweise vorsortierten Daten.
* Komplexität der Implementierung: Die Implementierung von Heapsort kann komplexer sein als die von einfacheren Algorithmen wie Selectionsort oder Insertion Sort.
* Höhere Anzahl an Vergleichen: Im Durchschnitt benötigt Heapsort mehr Vergleiche pro Element als einige andere Sortieralgorithmen, was zu einer schlechteren Leistung in der Praxis führen kann.

## Anwendung / Szenarien

### Große Datenmengen
Heapsort ist besonders geeignet für die Sortierung sehr großer Datenmengen, da er eine garantierte Laufzeit von O(n log n) bietet und in-place arbeitet, was den Speicherbedarf minimiert.

### Teure Vergleichsoperationen
Wenn die Vergleichsoperationen auf den zu sortierenden Daten relativ aufwendig sind, kann die Bottom-Up-Variante von Heapsort vorteilhaft sein, da sie im Durchschnitt weniger Vergleiche benötigt und somit effizienter arbeitet.

### Vorsortierte Daten
Heapsort ist vorteilhaft, wenn die Daten bereits teilweise vorsortiert sind, da er eine garantierte Worst-Case-Laufzeit von O(n log n) hat, im Gegensatz zu Algorithmen wie Quicksort, die in solchen Fällen schlechter abschneiden können.

### Stabilität der Laufzeit
In Anwendungen, in denen eine konsistente Laufzeit unabhängig von der Anordnung der Eingabedaten erforderlich ist, kann Heapsort eine gute Wahl sein, da er eine garantierte Laufzeit hat, die nicht von der spezifischen Datenanordnung abhängt.

### Vergleich mit anderen Algorithmen
Heapsort kann in Situationen eingesetzt werden, in denen andere Algorithmen wie Quicksort oder Introsort aufgrund ihrer schlechteren Worst-Case-Leistung (O(n²)) nicht geeignet sind, insbesondere wenn die Datenstruktur nicht optimal für diese Algorithmen ist.

## Impelmentierung

```C#
using System;

class Heapsort
{
    public static void Sort(int[] array)
    {
        int n = array.Length;

        // Schritt 1: Erstelle einen Max-Heap
        for (int i = n / 2 - 1; i >= 0; i--)
        {
            Heapify(array, n, i);
        }

        // Schritt 2: Extrahiere Elemente aus dem Heap
        for (int i = n - 1; i > 0; i--)
        {
            // Verschiebe das aktuelle Wurzelelement (größtes Element) ans Ende
            Swap(array, 0, i);

            // Rufe Heapify auf den reduzierten Heap auf
            Heapify(array, i, 0);
        }
    }

    // Hilfsfunktion, um einen Teil des Heaps zu erstellen
    private static void Heapify(int[] array, int n, int i)
    {
        int largest = i; // Initialisiere das größte Element als Wurzel
        int left = 2 * i + 1; // Linkes Kind
        int right = 2 * i + 2; // Rechtes Kind

        // Wenn das linke Kind größer ist als die Wurzel
        if (left < n && array[left] > array[largest])
        {
            largest = left;
        }

        // Wenn das rechte Kind größer ist als das größte bisher
        if (right < n && array[right] > array[largest])
        {
            largest = right;
        }

        // Wenn das größte Element nicht die Wurzel ist
        if (largest != i)
        {
            Swap(array, i, largest);

            // Rekursiv Heapify den betroffenen Teilbaum
            Heapify(array, n, largest);
        }
    }

    // Hilfsfunktion zum Vertauschen von zwei Elementen im Array
    private static void Swap(int[] array, int a, int b)
    {
        int temp = array[a];
        array[a] = array[b];
        array[b] = temp;
    }

    // Hauptprogramm zum Testen des Heapsort-Algorithmus
    public static void Main(string[] args)
    {
        int[] array = { 23, 1, 6, 19, 14, 18, 8, 24, 15 };
        Console.WriteLine("Unsortiertes Array:");
        Console.WriteLine(string.Join(", ", array));

        Sort(array);

        Console.WriteLine("Sortiertes Array:");
        Console.WriteLine(string.Join(", ", array));
    }
}
```

## Link

* [https://de.wikipedia.org/wiki/Heapsort](https://de.wikipedia.org/wiki/Heapsort)