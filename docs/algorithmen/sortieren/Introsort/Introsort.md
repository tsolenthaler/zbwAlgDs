# Introsort

* Hybrider Ansatz: Introsort beginnt mit Quicksort, um die Vorteile der schnellen durchschnittlichen Laufzeit zu nutzen. Wenn die Rekursionstiefe eine bestimmte Grenze überschreitet, wechselt der Algorithmus zu Heapsort, um die Worst-Case-Laufzeit zu garantieren.

* Rekursionstiefe: Introsort überwacht die Rekursionstiefe während des Sortierens. Diese Tiefe wird oft auf log(n) gesetzt, wobei n die Anzahl der Elemente ist. Wenn die Rekursionstiefe diese Grenze überschreitet, wird Heapsort verwendet.

* Laufzeit: Die durchschnittliche Laufzeit von Introsort ist O(nlogn), was es effizient macht. Im schlimmsten Fall hat es ebenfalls eine Laufzeit von O(nlogn), da Heapsort im schlimmsten Fall immer diese Laufzeit hat.

* In-Place-Sortierung: Introsort ist ein in-place Algorithmus, was bedeutet, dass er nur eine konstante Menge an zusätzlichem Speicher benötigt, unabhängig von der Eingabemenge.

* Stabilität: Introsort ist nicht stabil, was bedeutet, dass die relative Reihenfolge von gleichen Elementen nicht garantiert bleibt.

* Anpassungsfähigkeit: Introsort kann sich an die Struktur der Eingabedaten anpassen, da es die Vorteile von Quicksort in den besten Fällen und die Robustheit von Heapsort in den schlechtesten Fällen kombiniert.


## Vorteile:

* Effiziente durchschnittliche Laufzeit: Introsort hat eine durchschnittliche Laufzeit von O(nlogn), was ihn in den meisten Fällen sehr schnell macht.

* Schlimmster Fall Laufzeit: Im Gegensatz zu Quicksort, der im schlimmsten Fall O(n2) laufen kann, hat Introsort im schlimmsten Fall eine garantierte Laufzeit von O(nlogn), da er zu Heapsort wechselt.

* In-Place-Sortierung: Introsort benötigt nur eine konstante Menge an zusätzlichem Speicher, was ihn speichereffizient macht.

* Anpassungsfähigkeit: Der Algorithmus kann sich an die Struktur der Eingabedaten anpassen, indem er die Vorteile von Quicksort und Heapsort kombiniert.

* Einfachheit der Implementierung: Introsort ist relativ einfach zu implementieren, da es auf den bekannten Algorithmen Quicksort und Heapsort basiert.

## Nachteile:

* Nicht stabil: Introsort ist ein instabiler Sortieralgorithmus, was bedeutet, dass die relative Reihenfolge von gleichen Elementen nicht beibehalten wird. Dies kann in bestimmten Anwendungen problematisch sein.

* Heapsort-Performance: Obwohl Heapsort im schlimmsten Fall effizient ist, ist seine durchschnittliche Leistung oft schlechter als die von Quicksort. Dies kann dazu führen, dass Introsort in einigen Fällen langsamer ist, wenn er zu Heapsort wechselt.

* Konstante Rekursionstiefe: Die Wahl der maximalen Rekursionstiefe kann die Leistung beeinflussen. Eine falsche Wahl kann dazu führen, dass der Algorithmus unnötig oft zu Heapsort wechselt.

* Komplexität der Implementierung: Obwohl die Grundidee einfach ist, kann die Implementierung von Introsort komplexer sein als die von reinem Quicksort oder Heapsort, insbesondere wenn es um die Handhabung der Rekursionstiefe geht.


## Anwendung

### Einsatzbereiche von Introsort:

* Standardbibliotheken: Introsort wird häufig in den Standardbibliotheken moderner Programmiersprachen verwendet, wie z.B. in C++ (STL) für die std::sort-Funktion. Dies liegt an seiner Effizienz und der garantierten Worst-Case-Laufzeit.

* Datenverarbeitung: In Anwendungen, die große Datenmengen verarbeiten, wie Datenbanken oder Big Data-Analysen, kann Introsort aufgrund seiner Effizienz und In-Place-Eigenschaften nützlich sein.

* Echtzeitanwendungen: In Systemen, die eine schnelle Reaktion erfordern, kann Introsort eine gute Wahl sein, da es eine garantierte Laufzeit hat und sich an die Eingabedaten anpassen kann.

* Allgemeine Sortieraufgaben: Introsort eignet sich gut für allgemeine Sortieraufgaben, bei denen die Datenstruktur unbekannt ist und eine robuste Lösung benötigt wird.

### Abgrenzung zu anderen Sortieralgorithmen:

* Quicksort: Quicksort hat eine bessere durchschnittliche Laufzeit, kann jedoch im schlimmsten Fall O(n2) erreichen. Introsort kombiniert die Vorteile von Quicksort und Heapsort, um die Worst-Case-Leistung zu verbessern.

* Heapsort: Heapsort hat eine garantierte Worst-Case-Laufzeit von O(nlogn), ist jedoch in der Regel langsamer als Quicksort im Durchschnitt. Introsort verwendet Heapsort als Fallback, wenn die Rekursionstiefe zu hoch wird.

* Mergesort: Mergesort ist stabil und hat eine garantierte Laufzeit von O(nlogn), benötigt jedoch zusätzlichen Speicherplatz. Introsort ist in-place und daher speichereffizienter, aber nicht stabil.

* Timsort: Timsort, der in Python und Java verwendet wird, ist ein stabiler Sortieralgorithmus, der auf Mergesort basiert. Introsort ist nicht stabil, was ihn in Anwendungen, die Stabilität erfordern, weniger geeignet macht.


## Implementierung

```C#
using System;

public class Introsort
{
    private const int MaxDepthFactor = 2;

    public static void Sort(int[] array)
    {
        if (array == null || array.Length == 0)
            return;

        int maxDepth = (int)(Math.Log(array.Length) * MaxDepthFactor);
        IntrosortRecursive(array, 0, array.Length - 1, maxDepth);
    }

    private static void IntrosortRecursive(int[] array, int left, int right, int maxDepth)
    {
        if (right - left <= 16) // Switch to insertion sort for small arrays
        {
            InsertionSort(array, left, right);
            return;
        }

        if (maxDepth == 0)
        {
            Heapsort(array, left, right);
            return;
        }

        int pivotIndex = Partition(array, left, right);
        IntrosortRecursive(array, left, pivotIndex - 1, maxDepth - 1);
        IntrosortRecursive(array, pivotIndex + 1, right, maxDepth - 1);
    }

    private static int Partition(int[] array, int left, int right)
    {
        int pivot = array[right];
        int i = left - 1;

        for (int j = left; j < right; j++)
        {
            if (array[j] <= pivot)
            {
                i++;
                Swap(array, i, j);
            }
        }

        Swap(array, i + 1, right);
        return i + 1;
    }

    private static void Swap(int[] array, int i, int j)
    {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    private static void InsertionSort(int[] array, int left, int right)
    {
        for (int i = left + 1; i <= right; i++)
        {
            int key = array[i];
            int j = i - 1;

            while (j >= left && array[j] > key)
            {
                array[j + 1] = array[j];
                j--;
            }
            array[j + 1] = key;
        }
    }

    private static void Heapsort(int[] array, int left, int right)
    {
        int n = right - left + 1;

        for (int i = n / 2 - 1; i >= 0; i--)
            Heapify(array, n, i, left);

        for (int i = n - 1; i >= 0; i--)
        {
            Swap(array, left, left + i);
            Heapify(array, n, 0, left);
        }
    }

    private static void Heapify(int[] array, int n, int i, int left)
    {
        int largest = i;
        int leftChild = 2 * i + 1;
        int rightChild = 2 * i + 2;

        if (leftChild < n && array[left + leftChild] > array[left + largest])
            largest = leftChild;

        if (rightChild < n && array[left + rightChild] > array[left + largest])
            largest = rightChild;

        if (largest != i)
        {
            Swap(array, left + i, left + largest);
            Heapify(array, n, largest, left);
        }
    }
}

// Beispiel zur Verwendung
public class Program
{
    public static void Main()
    {
        int[] array = { 5, 2, 9, 1, 5, 6 };
        Introsort.Sort(array);
        Console.WriteLine(string.Join(", ", array));
    }
}
```



## Links

* [https://de.wikipedia.org/wiki/Introsort](https://de.wikipedia.org/wiki/Introsort)
