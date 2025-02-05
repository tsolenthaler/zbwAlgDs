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
| Bubblesort       | 𝑂(𝑛)          | 𝑂(𝑛²)         | 𝑂(𝑛²)         | ja     |
| Bucketsort       | 𝑂(𝑛)          | 𝑂(𝑛)          | 𝑂(𝑛²)         | (ja)   |
| Heapsort         | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | nein   |
| Insertionsort    | 𝑂(𝑛)          | 𝑂(𝑛²)         | 𝑂(𝑛²)         | ja     |
| Introsort        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | nein   |
| Mergesort        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | ja     |
| Quicksort        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛²)         | nein   |
| Selectionsort    | 𝑂(𝑛²)         | 𝑂(𝑛²)         | 𝑂(𝑛²)         | nein   |
| Shellsort        | 𝑂(𝑛 log 𝑛)    | 𝑂(𝑛¹.²⁵)      | 𝑂(𝑛¹.⁵)       | nein   |


## Zusammenfassung

* Auswahl allgemein anhand Komplexitätsklasse (WorstCase)
* Unter bestimmten Voraussetzungen sind jedoch evtl. andere Sortierverfahren schneller
    * Datenmenge
    * Verteilung der Daten
    * Vorsortiert (z.B. Bubblesort ist bei Einsortierung eines Elements schneller als Mergesort oder Quicksort)

### SORTIEREN MIT .NET