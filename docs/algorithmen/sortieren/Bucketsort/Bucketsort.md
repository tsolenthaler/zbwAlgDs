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

## Anwendung?

## Impelementierung?

## Links

* [https://de.wikipedia.org/wiki/Bucketsort](https://de.wikipedia.org/wiki/Bucketsort)