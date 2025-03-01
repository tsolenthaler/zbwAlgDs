# Bubblesort

## Vorteile von Bubblesort:

* Einfachheit: Bubblesort ist leicht zu verstehen und zu implementieren. Dies macht ihn zu einem guten Lehrwerkzeug für grundlegende Konzepte des Sortierens und der Algorithmusanalyse.

* Stabilität: Bubblesort ist ein stabiler Sortieralgorithmus, was bedeutet, dass die relative Reihenfolge von gleichwertigen Elementen beibehalten wird.

* In-Place-Sortierung: Der Algorithmus benötigt keinen zusätzlichen Speicherplatz, da er die Elemente innerhalb des ursprünglichen Arrays sortiert.

* Optimierungsmöglichkeiten: Durch die Implementierung einer Abbruchbedingung (wie im optimierten Bubblesort) kann die Laufzeit in Fällen, in denen die Liste bereits sortiert ist, auf O(n) reduziert werden.

* Geringe konstante Laufzeitfaktoren für kleine Eingaben: Bei kleinen Datensätzen kann Bubblesort aufgrund seiner einfachen Struktur und der geringen konstanten Faktoren effizienter sein als komplexere Algorithmen.

## Nachteile von Bubblesort:

* Schlechte Laufzeitkomplexität: Die Laufzeit von Bubblesort beträgt im schlimmsten und durchschnittlichen Fall O(n²), was ihn für große Datensätze ineffizient macht. Dies ist ein wesentlicher Nachteil im Vergleich zu anderen Sortieralgorithmen wie Quicksort oder Mergesort, die eine bessere asymptotische Laufzeit bieten.

* Hohe Anzahl an Vergleichen und Vertauschungen: Bubblesort führt im schlimmsten Fall eine große Anzahl von Vergleichen und Vertauschungen durch, was die Leistung weiter beeinträchtigt.

* Nicht optimal für große Datenmengen: Aufgrund seiner ineffizienten Laufzeit ist Bubblesort in der Praxis selten für große Datenmengen geeignet, da andere Algorithmen deutlich schneller sind.

* Langsame Anpassung an teilweise sortierte Listen: Obwohl Bubblesort in bestimmten Fällen optimiert werden kann, bleibt die Anpassung an teilweise sortierte Listen im Vergleich zu anderen Algorithmen wie Insertionsort suboptimal.

## Anwendung

### Einsatzbereiche von Bubblesort:

* Lehrzwecke: Bubblesort wird häufig in der Ausbildung verwendet, um grundlegende Konzepte des Sortierens, der Algorithmusanalyse und der Laufzeitanalyse zu vermitteln. Aufgrund seiner einfachen Struktur ist er leicht zu erklären und zu demonstrieren.

* Kleine Datensätze: Bubblesort kann für kleine Eingaben in Betracht gezogen werden, da die konstanten Laufzeitfaktoren eines Sortieralgorithmus bei kleinen n dominieren. In solchen Fällen kann Bubblesort effizienter sein als komplexere Algorithmen.

* Teilweise sortierte Listen: Wenn die Elemente einer Liste bereits nah an ihren endgültigen Positionen sind, kann Bubblesort aufgrund seiner optimierten Versionen (z. B. mit einer Abbruchbedingung) eine bessere Laufzeit als O(n²) erreichen, was ihn in solchen Szenarien nützlich macht.

### Abgrenzung von Bubblesort:

* Vergleich zu anderen Sortieralgorithmen: Bubblesort ist asymptotisch nicht optimal, insbesondere im Vergleich zu effizienteren Algorithmen wie Quicksort oder Mergesort, die eine Laufzeit von O(n log n) im besten Fall bieten. Daher wird Bubblesort in der Praxis selten für große Datensätze eingesetzt.

* Stabilität und In-Place-Sortierung: Obwohl Bubblesort stabil und in-place ist, haben andere Algorithmen wie Insertionsort ähnliche Eigenschaften, jedoch mit besseren konstanten Laufzeitfaktoren.

* Einschränkungen bei großen Datenmengen: Aufgrund seiner hohen Laufzeitkomplexität (O(n²) im schlimmsten und durchschnittlichen Fall) ist Bubblesort für große Datenmengen ungeeignet. In solchen Fällen sind effizientere Algorithmen vorzuziehen.

* Optimierte Varianten: Es gibt optimierte Versionen von Bubblesort, die versuchen, die Laufzeit in bestimmten Szenarien zu verbessern, jedoch bleibt die Grundstruktur des Algorithmus ineffizient im Vergleich zu anderen modernen Sortieralgorithmen.

## Implementierung

```C#
using System;

class Program
{
    static void Main()
    {
        int[] array = { 64, 34, 25, 12, 22, 11, 90 };
        
        Console.WriteLine("Unsortiertes Array:");
        PrintArray(array);
        
        BubbleSort(array);
        
        Console.WriteLine("Sortiertes Array:");
        PrintArray(array);
    }

    static void BubbleSort(int[] arr)
    {
        int n = arr.Length;
        bool swapped;

        // Äußere Schleife für die Anzahl der Durchläufe
        for (int i = 0; i < n - 1; i++)
        {
            swapped = false;

            // Innere Schleife für den Vergleich und das Vertauschen
            for (int j = 0; j < n - i - 1; j++)
            {
                if (arr[j] > arr[j + 1])
                {
                    // Vertauschen, wenn das Element gefunden wird, das größer ist als das nächste
                    Swap(ref arr[j], ref arr[j + 1]);
                    swapped = true;
                }
            }

            // Wenn in diesem Durchlauf keine Vertauschungen stattfanden, ist das Array bereits sortiert
            if (!swapped)
                break;
        }
    }

    static void Swap(ref int a, ref int b)
    {
        int temp = a;
        a = b;
        b = temp;
    }

    static void PrintArray(int[] arr)
    {
        foreach (int value in arr)
        {
            Console.Write(value + " ");
        }
        Console.WriteLine();
    }
}
```

### Implementierung der Optimierten Variante

```C#
using System;

class Program
{
    static void Main()
    {
        int[] array = { 64, 34, 25, 12, 22, 11, 90 };
        
        Console.WriteLine("Unsortiertes Array:");
        PrintArray(array);
        
        OptimizedBubbleSort(array);
        
        Console.WriteLine("Sortiertes Array:");
        PrintArray(array);
    }

    static void OptimizedBubbleSort(int[] arr)
    {
        int n = arr.Length;
        bool swapped;

        // Äußere Schleife für die Anzahl der Durchläufe
        for (int i = 0; i < n - 1; i++)
        {
            swapped = false;

            // Innere Schleife für den Vergleich und das Vertauschen
            for (int j = 0; j < n - i - 1; j++)
            {
                if (arr[j] > arr[j + 1])
                {
                    // Vertauschen, wenn das Element gefunden wird, das größer ist als das nächste
                    Swap(ref arr[j], ref arr[j + 1]);
                    swapped = true;
                }
            }

            // Wenn in diesem Durchlauf keine Vertauschungen stattfanden, ist das Array bereits sortiert
            if (!swapped)
                break;
        }
    }

    static void Swap(ref int a, ref int b)
    {
        int temp = a;
        a = b;
        b = temp;
    }

    static void PrintArray(int[] arr)
    {
        foreach (int value in arr)
        {
            Console.Write(value + " ");
        }
        Console.WriteLine();
    }
}
```

## Links

* [Wikipedia](https://de.wikipedia.org/wiki/Bubblesort)
* [https://studyflix.de/informatik/bubblesort-1325](https://studyflix.de/informatik/bubblesort-1325)