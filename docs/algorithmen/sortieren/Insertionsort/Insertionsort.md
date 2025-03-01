# Insertionsort

## Vorteile von Insertionsort:

* Einfachheit der Implementierung: Insertionsort ist leicht zu verstehen und zu implementieren, was es zu einer guten Wahl für einfache Sortieraufgaben macht.
* Stabilität: Das Verfahren ist stabil, d.h. die Reihenfolge von Elementen mit gleichem Schlüsselwert bleibt unverändert.
* Effizienz bei kleinen oder teilweise sortierten Daten: Insertionsort ist besonders effizient, wenn die Eingabemenge klein oder bereits teilweise sortiert ist. In solchen Fällen kann die Laufzeit deutlich unter O(n²) liegen.
* In-Place-Sortierung: Der Algorithmus benötigt keinen zusätzlichen Speicherplatz, da er in-place arbeitet, was bedeutet, dass die Sortierung direkt im ursprünglichen Array erfolgt.
* Online-Algorithmus: Insertionsort kann als Online-Algorithmus verwendet werden, was bedeutet, dass es Elemente sortieren kann, während sie eintreffen.

## Nachteile von Insertionsort:

* Ineffizienz bei großen Datenmengen: Im Vergleich zu anderen, komplexeren Sortierverfahren (wie Quicksort, Mergesort oder Heapsort) ist Insertionsort weniger effizient, insbesondere bei großen unsortierten Datenmengen, da die durchschnittliche und schlechteste Laufzeit O(n²) beträgt.
* Hohe Anzahl an Vergleichen und Verschiebungen: Die Anzahl der Vergleiche und Verschiebungen hängt stark von der Anordnung der Elemente ab. Im schlechtesten Fall (z.B. bei einem absteigend sortierten Array) sind viele Verschiebungen erforderlich, was die Leistung beeinträchtigt.
* Schwierige Abschätzung der Laufzeit im Durchschnittsfall: Die Laufzeit im Durchschnittsfall ist schwer genau abzuschätzen, was die Vorhersagbarkeit der Leistung des Algorithmus einschränkt.

## Anwendung

### Einsatzbereiche von Insertionsort:

* Kleine Datensätze: Insertionsort ist besonders effizient bei kleinen Datensätzen. Bei einer geringen Anzahl von Elementen (z. B. weniger als 20) kann Insertionsort schneller sein als komplexere Algorithmen, da die konstanten Faktoren und die einfache Implementierung den Overhead der anderen Algorithmen überwiegen.

* Teilweise sortierte Daten: Wenn die Eingabedaten bereits teilweise sortiert sind, kann Insertionsort sehr schnell arbeiten, da es in solchen Fällen weniger Vergleiche und Verschiebungen benötigt. In der besten Fall-Situation (bereits sortiert) hat der Algorithmus eine lineare Laufzeit von O(n).

* Echtzeit- oder Online-Anwendungen: Insertionsort kann in Szenarien eingesetzt werden, in denen Daten kontinuierlich eintreffen und sofort sortiert werden müssen. Da es als Online-Algorithmus funktioniert, kann es neue Elemente sofort in die bereits sortierte Liste einfügen.

* Stabile Sortierung erforderlich: In Anwendungen, in denen die Stabilität der Sortierung wichtig ist (d.h. die relative Reihenfolge von gleichwertigen Elementen beibehalten werden muss), ist Insertionsort eine geeignete Wahl.

* Einfache Implementierung: In Lehr- und Lernkontexten wird Insertionsort häufig verwendet, um grundlegende Konzepte der Sortierung und Algorithmen zu vermitteln, da es einfach zu verstehen und zu implementieren ist.

### Abgrenzung von Insertionsort:

* Große Datensätze: Bei großen Datensätzen ist Insertionsort in der Regel ineffizient, da seine durchschnittliche und schlechteste Laufzeit O(n²) beträgt. In solchen Fällen sind Algorithmen wie Quicksort, Mergesort oder Heapsort vorzuziehen, die eine bessere Leistung bieten.

* Komplexe Datenstrukturen: In Anwendungen, die komplexe Datenstrukturen oder große Mengen an Daten erfordern, sind fortgeschrittene Sortieralgorithmen, die auf Divide-and-Conquer-Strategien basieren, oft die bessere Wahl.

* Häufige Sortieroperationen: Wenn häufige Sortieroperationen auf großen Datenmengen erforderlich sind, sind Algorithmen, die eine bessere durchschnittliche Laufzeit bieten, wie Mergesort oder Heapsort, geeigneter.

* Nicht-stabile Sortierung: In Fällen, in denen die Stabilität der Sortierung nicht erforderlich ist, können andere Algorithmen, die möglicherweise schneller sind, bevorzugt werden.

## Impelmentierung

```C#
using System;

class Program
{
    static void Main()
    {
        int[] array = { 5, 2, 4, 6, 1, 3 };
        Console.WriteLine("Unsortiertes Array:");
        PrintArray(array);

        InsertionSort(array);

        Console.WriteLine("Sortiertes Array:");
        PrintArray(array);
    }

    static void InsertionSort(int[] array)
    {
        int n = array.Length;

        for (int i = 1; i < n; i++)
        {
            int einzusortierenderWert = array[i];
            int j = i - 1;

            // Verschiebe die Elemente, die größer als der einzusortierende Wert sind,
            // um eine Position nach hinten
            while (j >= 0 && array[j] > einzusortierenderWert)
            {
                array[j + 1] = array[j];
                j--;
            }
            // Füge den einzusortierenden Wert an der richtigen Position ein
            array[j + 1] = einzusortierenderWert;
        }
    }

    static void PrintArray(int[] array)
    {
        foreach (int value in array)
        {
            Console.Write(value + " ");
        }
        Console.WriteLine();
    }
}
```

## Links

* [Wikipedia](https://de.wikipedia.org/wiki/Insertionsort)
* [https://studyflix.de/informatik/insertionsort-1321](https://studyflix.de/informatik/insertionsort-1321)
