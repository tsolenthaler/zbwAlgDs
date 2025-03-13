# Bucketsort

Bucketsort (von englisch bucket „Eimer“) ist ein Sortierverfahren, das für bestimmte Werte-Verteilungen eine Eingabe-Liste in linearer Zeit sortiert. Der Algorithmus ist in drei Phasen eingeteilt:

1. Verteilung der Elemente auf die Buckets (Partitionierung)
2. Jeder Bucket wird mit einem weiteren Sortierverfahren wie beispielsweise Mergesort sortiert.
3. Der Inhalt der sortierten Buckets wird konkateniert.

Das Verfahren arbeitet also out-of-place. 

## Algorithmus

Die Eingabe von Bucketsort ist eine Liste l mit n Elementen und eine Funktion f, die jedes Element der Liste in das halboffene Intervall [ 0 , 1 [ monoton in der Weise abbildet, dass f(e)≤f(e′) für e  sortiermäßig ≺ e′. Basiert die Sortierreihenfolge ≺ auf einem Vergleich binärer Daten, kann man die Bits mit der höchsten Signifikanz nehmen. Während der Sortierung verwendet der Algorithmus k „Buckets“, die in einem Array angeordnet sind. Die Verteilung der Elemente geschieht über dieses Array, indem jedes Element e in den  ⌊f(e)⋅k⌋ -ten Bucket gelegt wird. Danach wird nacheinander jeder Bucket sortiert. In der letzten Phase werden die Bucket-Listen in der Reihenfolge, wie sie im Array angeordnet sind, konkateniert, was als Ergebnis die sortierte Ausgabe darstellt.

## Pseudo-Code
```
 bucket_sort(l, f, k)
   buckets = array(k)
   foreach (e in l)
     buckets[ floor(f(e) * k) ].add(e)
   r = []
   foreach (b in buckets)
     x = mergesort(b)
     r.append(x)
   return r
```
Der Algorithmus sortiert stabil, wenn der für die Sortierung der Buckets verwendete Sortier-Algorithmus, hier mergesort, stabil ist. 

## Komplexität

Die Verteilung der Funktionswerte von f bestimmt die Laufzeit von Bucketsort. Die Laufzeit ist in O ( n ) + ∑ i = 0 k − 1 O ( l i log ⁡ l i ) (in O-Notation), wobei l i {\displaystyle l_{i}} die Anzahl der Elemente im i-ten Bucket bezeichnet. Bei einer Gleichverteilung ist die Gesamtlaufzeit in O ( n ), da die Summe über die Buckets linear ist und ihre Summanden als konstant (bei exakter Gleichverteilung =1) angesehen werden können. Die effiziente Laufzeit von O ( n ) ist nicht nur bei einer Gleichverteilung gegeben, sondern bei allen Verteilungen, nach denen der Summenterm asymptotisch linear ist. Sie wird auch als Average-Case-Laufzeit angesehen.

Bei anderen Werte-Verteilungen kann die Laufzeit des Bucketsortalgorithmus von der Laufzeit des Sortier-Algorithmus dominiert werden, der zur Sortierung eines Buckets verwendet wird. Ein solcher Worst-Case tritt beispielsweise ein, wenn alle Elemente einem einzigen Bucket zugeordnet werden. Bei Verwendung von mergesort für die Sortierung der Buckets ist die Gesamtlaufzeit dann in O ( n log ⁡n ).

Natürlich lässt sich diese Sortierung zweiter Stufe wieder als Bucketsort implementieren, dann mit Sub-Buckets pro Bucket. Diese Vorgehensweise ist im Artikel Radixsort beschrieben und ist eine Form des MSD Radixsort.

Der Speicherbedarf liegt in O (n). 

## Vorteile

* Lineare Laufzeit: Bei gleichmäßiger Verteilung der Elemente kann Bucketsort in linearer Zeit (O(n)) arbeiten.
* Stabilität: Der Algorithmus kann stabil sortieren, wenn ein stabiler Sortieralgorithmus (wie Mergesort) für die Sortierung der Buckets verwendet wird.
* Effiziente Verarbeitung: Bei bestimmten Verteilungen, bei denen die Summe der Elemente in den Buckets asymptotisch linear ist, bleibt die Laufzeit ebenfalls in O(n).
*  Flexibilität: Bucketsort kann mit verschiedenen Sortieralgorithmen für die Buckets kombiniert werden, was Anpassungen an spezifische Anforderungen ermöglicht.
* Geringer Speicherbedarf: Der Speicherbedarf liegt in O(n), was für große Datenmengen vorteilhaft ist.

## Nachteile:

* Abhängigkeit von der Verteilung: Die Effizienz des Algorithmus hängt stark von der Verteilung der Eingabewerte ab; bei ungünstigen Verteilungen kann die Laufzeit erheblich steigen.
* Worst-Case-Szenario: Wenn alle Elemente in einen einzigen Bucket fallen, kann die Laufzeit auf O(n log n) ansteigen, was die Vorteile der linearen Laufzeit zunichte macht.
* Out-of-Place: Bucketsort arbeitet out-of-place, was bedeutet, dass zusätzlicher Speicher benötigt wird, um die Buckets zu speichern.
* Komplexität der Implementierung: Die Implementierung kann komplexer sein als bei anderen Sortieralgorithmen, insbesondere wenn mehrere Sortierstufen (Sub-Buckets) erforderlich sind.
* Eingeschränkte Anwendbarkeit: Bucketsort ist am effektivsten für Daten, die in einem bestimmten Intervall liegen und gleichmäßig verteilt sind, was seine Anwendbarkeit einschränken kann.

## Anwendung

Der Bucket Sort-Algorithmus ist ein nicht vergleichender Sortieralgorithmus, der in bestimmten Szenarien besonders effektiv ist. Hier sind einige Einsatzbereiche und Abgrenzungen des Bucket Sort:

### Einsatzbereiche

1. **Gleichmäßig verteilte Daten**:
   - Bucket Sort ist besonders effizient, wenn die Eingabedaten gleichmäßig über einen bestimmten Bereich verteilt sind. Zum Beispiel kann er gut für Daten verwendet werden, die aus einer gleichmäßigen Verteilung stammen, wie z.B. Fließkommazahlen im Bereich von 0 bis 1.

2. **Daten mit begrenztem Wertebereich**:
   - Wenn die Daten einen begrenzten Wertebereich haben, kann Bucket Sort sehr schnell sein, da die Anzahl der Buckets (k) im Vergleich zur Anzahl der Elemente (n) klein gehalten werden kann.

3. **Daten mit bekannten Eigenschaften**:
   - In Anwendungen, in denen die Verteilung der Daten bekannt ist (z.B. Noten, Messwerte), kann Bucket Sort verwendet werden, um die Sortierung zu optimieren.

4. **Parallelverarbeitung**:
   - Da die Buckets unabhängig voneinander sortiert werden können, eignet sich Bucket Sort gut für parallele oder verteilte Systeme, wo die Sortierung der einzelnen Buckets gleichzeitig durchgeführt werden kann.

5. **Echtzeitanwendungen**:
   - In Anwendungen, die eine schnelle Sortierung erfordern, wie z.B. in der Grafikanalyse oder bei der Verarbeitung von Streaming-Daten, kann Bucket Sort nützlich sein.

### Abgrenzung

1. **Vergleichsbasierte Sortieralgorithmen**:
   - Bucket Sort ist ein nicht vergleichender Algorithmus, was bedeutet, dass er nicht auf Vergleichen zwischen den Elementen basiert. Im Gegensatz dazu verwenden viele gängige Sortieralgorithmen wie Quicksort, Mergesort und Heapsort Vergleiche, um die Elemente zu sortieren.

2. **Effizienz bei ungleichmäßiger Verteilung**:
   - Wenn die Daten ungleichmäßig verteilt sind, kann Bucket Sort ineffizient werden, da einige Buckets möglicherweise viele Elemente enthalten, während andere leer bleiben. In solchen Fällen kann die Leistung von Bucket Sort schlechter sein als die von Vergleichsalgorithmen.

3. **Speicherbedarf**:
   - Bucket Sort benötigt zusätzlichen Speicherplatz für die Buckets, was in Situationen mit begrenztem Speicher problematisch sein kann. Im Vergleich dazu arbeiten einige Vergleichsalgorithmen in-place und benötigen weniger zusätzlichen Speicher.

4. **Komplexität**:
   - Die durchschnittliche Zeitkomplexität von Bucket Sort ist O(n + k), wobei n die Anzahl der Elemente und k die Anzahl der Buckets ist. Im schlimmsten Fall kann die Zeitkomplexität jedoch O(n^2) betragen, wenn alle Elemente in denselben Bucket fallen. Vergleichsbasierte Algorithmen haben in der Regel eine Zeitkomplexität von O(n log n).

### Fazit
Bucket Sort ist ein leistungsfähiger Algorithmus für spezifische Anwendungsfälle, insbesondere bei gleichmäßig verteilten Daten. Es ist jedoch wichtig, die Eigenschaften der Daten und die Anforderungen der Anwendung zu berücksichtigen, um zu entscheiden, ob Bucket Sort die beste Wahl ist oder ob ein anderer Sortieralgorithmus geeigneter wäre.

## Impelementierung
```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Beispiel-Array
        List<double> l = new List<double> { 0.78, 0.17, 0.39, 0.26, 0.72, 0.94, 0.21, 0.55, 0.88, 0.99 };
        int k = 5; // Anzahl der Buckets

        List<double> sortedList = BucketSort(l, k);
        
        Console.WriteLine("Sortierte Liste:");
        foreach (var item in sortedList)
        {
            Console.WriteLine(item);
        }
    }

    static List<double> BucketSort(List<double> l, int k)
    {
        // Erstellen der Buckets
        List<List<double>> buckets = new List<List<double>>(new List<double>[k]);
        for (int i = 0; i < k; i++)
        {
            buckets[i] = new List<double>();
        }

        // Verteilung der Elemente in die Buckets
        foreach (double e in l)
        {
            int bucketIndex = (int)Math.Floor(f(e) * k);
            if (bucketIndex >= k) bucketIndex = k - 1; // Sicherstellen, dass der Index im gültigen Bereich bleibt
            buckets[bucketIndex].Add(e);
        }

        // Sortieren der Buckets und Zusammenführen der Ergebnisse
        List<double> r = new List<double>();
        foreach (List<double> b in buckets)
        {
            b.Sort(); // Sortieren des Buckets
            r.AddRange(b); // Hinzufügen der sortierten Elemente zum Ergebnis
        }

        return r;
    }

    // Normalisierungsfunktion
    static double f(double e)
    {
        return e; // Hier könnte eine andere Normalisierungslogik implementiert werden
    }
}
```

## Links

* [https://de.wikipedia.org/wiki/Bucketsort](https://de.wikipedia.org/wiki/Bucketsort)