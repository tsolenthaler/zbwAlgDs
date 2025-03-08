# Implementierungen

## Ganzzahlen 
Hier ist eine Implementierung des Quicksort-Algorithmus in C# zur Sortierung einer Liste von Ganzzahlen:

```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<int> numbers = new List<int> { 34, 7, 23, 32, 5, 62 };
        Console.WriteLine("Unsortierte Liste: " + string.Join(", ", numbers));

        QuickSort(numbers, 0, numbers.Count - 1);

        Console.WriteLine("Sortierte Liste: " + string.Join(", ", numbers));
    }

    static void QuickSort(List<int> list, int low, int high)
    {
        if (low < high)
        {
            int pivotIndex = Partition(list, low, high);
            QuickSort(list, low, pivotIndex - 1);
            QuickSort(list, pivotIndex + 1, high);
        }
    }

    static int Partition(List<int> list, int low, int high)
    {
        int pivot = list[high]; // Wählen Sie das letzte Element als Pivot
        int i = low - 1; // Index des kleineren Elements

        for (int j = low; j < high; j++)
        {
            // Wenn das aktuelle Element kleiner oder gleich dem Pivot ist
            if (list[j] <= pivot)
            {
                i++;
                Swap(list, i, j); // Tauschen
            }
        }
        Swap(list, i + 1, high); // Pivot an die richtige Position setzen
        return i + 1; // Rückgabe des Index des Pivot-Elements
    }

    static void Swap(List<int> list, int i, int j)
    {
        int temp = list[i];
        list[i] = list[j];
        list[j] = temp;
    }
}
```