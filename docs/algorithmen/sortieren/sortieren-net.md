# Sortieren mit .Net

## Ziele

- [ ] Ich kenne die Komplexitätseigenschaften der Sortieralgorithmen
- [ ] Ich kenne Kriterien, die für die Entscheidung für den richtigen Sortieralgorithmus relevant sind
- [ ] Ich weiß, wie sie mit .NET Collections sortieren können
- [ ] Ich weiß, wie sie mit LINQ sortieren können
- [ ] Ich kenne die Mechanismen, die .NET für die Sortierung verwendet

## Übersicht

| Sortierverfahren | BestCase       | AverageCase    | WorstCase      | stabil |
|------------------|----------------|----------------|----------------|--------|
| [Bubblesort](Bubblesort/Bubblesort.md)       | 𝑂(𝑛)          | 𝑂(𝑛²)         | 𝑂(𝑛²)         | ja     |
| [Bucketsort](Bucketsort/Bucketsort.md)       | 𝑂(𝑛)          | 𝑂(𝑛)          | 𝑂(𝑛²)         | (ja)   |
| [Heapsort](Heapsort/Heapsort.md)         | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | nein   |
| [Insertionsort](Insertionsort/Insertionsort.md)    | 𝑂(𝑛)          | 𝑂(𝑛²)         | 𝑂(𝑛²)         | ja     |
| [Introsort](Introsort/Introsort.md)        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | nein   |
| [Mergesort](Mergesort/Mergesort.md)        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | ja     |
| [Quicksort](Quicksort/Quicksort.md)        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛²)         | nein   |
| [Selectionsort](Selectionsort/Selectionsort.md)    | 𝑂(𝑛²)         | 𝑂(𝑛²)         | 𝑂(𝑛²)         | nein   |
| [Shellsort](Shellsort/Shellsort.md)        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛¹.²⁵)      | 𝑂(𝑛¹.⁵)       | nein   |


## Zusammenfassung

* Auswahl allgemein anhand Komplexitätsklasse (WorstCase)
* Unter bestimmten Voraussetzungen sind jedoch evtl. andere Sortierverfahren schneller
    * Datenmenge
    * Verteilung der Daten
    * Vorsortiert (z.B. Bubblesort ist bei Einsortierung eines Elements schneller als Mergesort oder Quicksort)

## SORTIEREN MIT .NET

### Collections sortieren

* List<T>.Sort(), ArrayList.Sort()
    * verwendet Array.Sort()
    * Introsort
        * Wenn die Grösse der Partition <16 Elemente: Insertionsort
            * -> Wieso?
        * Wenn die Rekursionstiefe des Quicksorts >2*log n: Heapsort
            * -> Wieso?
        * Andernfalls: Quicksort
    * instabiles Verfahren
    * Elemente müssen das Interface IComparable implementieren. So können auch beliebige Objekte sortiert werden
    * Überladung, bei der IComparer-Objekt übergeben werden kann. Dann wird dieser verwendet anstatt Icomparable

### Collections sortieren

* SortedList<TKey, TValue>(), SortedDictionary<TKey, TValue>()
    * Sortiert nach Key anhand IComparer<TKey>

### LINQ 🔴

### Üben!! 🔴

* BubbleSort
* MergeSort parallel ausführen

### Aufgabe
* Implementieren Sie eine Klasse Person mit den Eigenschaften Name, Vorname und Grösse
* Erstellen sie eine Liste von verschiedenen Personen
* Wenden Sie List<Person>.Sort() an: Sortieren Sie einmal nach Name+Vorname und einmal nach Grösse