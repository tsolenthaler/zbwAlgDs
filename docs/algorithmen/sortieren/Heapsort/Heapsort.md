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
    public static void Heapsort(int[] A)
    {
        // Schritt 1: Erstelle einen Max-Heap
        BuildHeap(A);
        AssertIsHeap(A, 0);

        int tmp = A.Length; // Speichere die ursprüngliche Größe des Arrays

        // Schritt 2: Sortiere das Array
        while (A.Length > 1)
        {
            Swap(A, 0, A.Length - 1); // Vertausche das größte Element mit dem letzten Element
            Array.Resize(ref A, A.Length - 1); // Verringere die Größe des Arrays
            Heapify(A); // Stelle den Heap wieder her
            AssertIsHeap(A, 0);
        }

        // Stelle die ursprüngliche Größe des Arrays wieder her (optional, je nach Bedarf)
        Array.Resize(ref A, tmp);
        AssertIsSorted(A);
    }

    private static void BuildHeap(int[] A)
    {
        int n = A.Length;
        for (int i = n / 2 - 1; i >= 0; i--)
        {
            Heapify(A, n, i);
        }
    }

    private static void Heapify(int[] A, int n, int i)
    {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < n && A[left] > A[largest])
        {
            largest = left;
        }

        if (right < n && A[right] > A[largest])
        {
            largest = right;
        }

        if (largest != i)
        {
            Swap(A, i, largest);
            Heapify(A, n, largest);
        }
    }

    private static void Swap(int[] A, int a, int b)
    {
        int temp = A[a];
        A[a] = A[b];
        A[b] = temp;
    }

    private static void AssertIsHeap(int[] A, int index)
    {
        // Hier könnte eine Implementierung zur Überprüfung der Heap-Eigenschaft stehen
        // Diese Methode ist nur ein Platzhalter
    }

    private static void AssertIsSorted(int[] A)
    {
        // Hier könnte eine Implementierung zur Überprüfung der Sortierung stehen
        // Diese Methode ist nur ein Platzhalter
    }

    // Hauptprogramm zum Testen des Heapsort-Algorithmus
    public static void Main(string[] args)
    {
        int[] array = { 23, 1, 6, 19, 14, 18, 8, 24, 15 };
        Console.WriteLine("Unsortiertes Array:");
        Console.WriteLine(string.Join(", ", array));

        Heapsort(array);

        Console.WriteLine("Sortiertes Array:");
        Console.WriteLine(string.Join(", ", array));
    }
}
```

### Impelmentierung Bottom-Up-Heapsort

```C#
using System;

class Heapsort
{
    public static int HeapsortBu(int[] data, int n) // zu sortierendes Feld und seine Länge
    {
        int val, parent, child;
        int root = n >> 1; // erstes Blatt im Baum
        int count = 0; // Zähler für Anzahl der Vergleiche

        while (true)
        {
            if (root > 0) // Teil 1: Konstruktion des Heaps
            {
                parent = --root;
                val = data[root]; // zu versickernder Wert
            }
            else if (--n > 0) // Teil 2: eigentliche Sortierung
            {
                val = data[n]; // zu versickernder Wert vom Heap-Ende
                data[n] = data[0]; // Spitze des Heaps hinter den Heap in den sortierten Bereich verschieben
                parent = 0; // zurück zur Wurzel
            }
            else // Heap ist leer; Sortierung beendet
            {
                break;
            }

            while ((child = (parent + 1) << 1) < n) // zweites Kind; Abbruch am Ende des Heaps
            {
                if (++count, data[child - 1] > data[child]) // größeres Kind wählen
                    --child;

                data[parent] = data[child]; // größeres Kind nach oben rücken
                parent = child; // in der Ebene darunter weitersuchen
            }

            if (child == n) // ein einzelnes Kind am Heap-Ende ist übersprungen worden
            {
                if (++count, data[--child] >= val) // größer als der zu versickernde Wert
                {
                    data[parent] = data[child]; // noch nach oben
                    data[child] = val; // versickerten Wert eintragen
                    continue;
                }

                child = parent; // 1 Ebene nach oben zurück
            }
            else
            {
                if (++count, data[parent] >= val) // das Blatt ist größer als der zu versickernde Wert
                {
                    data[parent] = val; // direkt eintragen
                    continue; // direkt eintragen
                }

                child = (parent - 1) >> 1; // 2 Ebenen nach oben zurück
            }

            while (child != root) // maximal zum Ausgangspunkt zurück
            {
                parent = (child - 1) >> 1; // den Vergleichswert haben wir bereits nach oben verschoben
                if (++count, data[parent] >= val) // größer als der zu versickernde Wert
                    break; // Position gefunden

                data[child] = data[parent]; // Rückverschiebung nötig
                child = parent; // 1 Ebene nach oben zurück
            }

            data[child] = val; // versickerten Wert eintragen
        }

        return count; // Anzahl der Vergleiche zurückgeben
    }

    // Hauptprogramm zum Testen des Heapsort-Algorithmus
    public static void Main(string[] args)
    {
        int[] array = { 23, 1, 6, 19, 14, 18, 8, 24, 15 };
        Console.WriteLine("Unsortiertes Array:");
        Console.WriteLine(string.Join(", ", array));

        int comparisons = HeapsortBu(array, array.Length);

        Console.WriteLine("Sortiertes Array:");
        Console.WriteLine(string.Join(", ", array));
        Console.WriteLine($"Anzahl der Vergleiche: {comparisons}");
    }
}
```

## Link

* [https://de.wikipedia.org/wiki/Heapsort](https://de.wikipedia.org/wiki/Heapsort)