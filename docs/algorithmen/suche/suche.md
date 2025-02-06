# Suche

## Ziele

- [ ] Ich kennen die zwei grundlegenden Suchalgorithmen
    - [ ]  LinearSearch
    - [ ]  BinarySearch
- [ ] Ich weiss, wie Sie die lineare Suche optimieren können
- [ ] Ich kennen die Komplexitätsklassen der beiden Algorithmen
- [ ] Ich weiss, welche Suchalgorithmen das .NET-Framework implementiert

## Grundlagen
* Suchen ist eine der häufigsten Operationen mit dem Computer
* Finden der richtigen Informationen in einer Menge von Daten
    * Name → Mitgliedernummer
    * Kontonummer (EC-Karte) → Konto
    * Telefonnummer → Name

### Lineare Suche
* Sequentielle Suche
* Start am Anfang der Liste
* Jedes Element wird geprüft

``` mermaid
flowchart LR
    1[Stop] --> 2[Wert gefunden] --> 3[→ erfolgreiche Suche]
    1[Stop] --> 4[Ende der Liste erreicht] --> 5[→ erfolglose Suche]
```
#### Komplexität der linearen Suche

* Best Case
    * Gesuchter Wert befindet sich an Position 1
    * 𝑂(1)
* Worst Case
    * Gesuchter Wert befindet sich nicht in der Liste
    * 𝑂(𝑛)
* Average Case
    * Um ein Element an der i-ten Position zu finden: i Vergleiche
    * Durchschnittliche Anzahl Vergleiche

Formel:
![Formel linearen Suche](formelLineareSuche.png)

#### Lineare Suche mit Sentinel

2 Vergleiche pro Loop

Total 2n Vergleiche

Optimierungspotential?

```C#
for (var i = 0; i < a.Length; i++) {
    if (a[i] == searchvalue) {
        return i;
    }
}
```

#### Lineare Suche in sortiertem Array

* Array nicht sortiert
    * Worst Case
        * ganzes Array muss durchlaufen werden
* Array sortiert
    * Worst Case
        * Array muss bis zum ersten Element, welches grösser ist, durchlaufen werden
* Vergleiche im Falle einer erfolglosen Suche werden reduziert

### Binäre Suche

* Voraussetzung: Sortiertes Array
* Prinzip: Divide and Conquer
* Prozedur
    * Vergleiche den gesuchten Wert mit dem mittleren Element des Arrays
    * Wenn gleich
        * Suche erfolgreich
    * Wenn kleiner
        * Weiter in der linken Hälfte
    * Wenn grösser
        * Weiter in der rechten Hälfte
* Wiederhole
* Process stoppt, wenn gefunden oder Teilarray hat Länge 0

#### Komplexität der binären Suche

* Best Case
    * Gesuchter Wert befindet sich in der Mitte der Liste
    * 𝑂(1)
* Worst Case
    * Gesuchter Wert befindet sich nicht in der Liste
    * 𝑂(log 𝑛) – Erklärung siehe Slides zu Performance
* Average Case
    * 𝑂(log 𝑛) – Die Mathematik ersparen wir uns

* Zusätzlicher Aufwand fürs Sortieren
    * 𝑂(𝑛 log 𝑛)

#### .NET

* List<T>.BinarySearch(T item)
    * Liste muss sortiert sein (siehe Dokumentation)
    * Aufgabe: Was steht hier in idx und wieso?

```C#
var list = new List<int> { 4, 2, 3, 7, 10, 5 };
var idx = list.BinarySearch(5);
```

* List<T>.Sort()
    * Introsort
        * Wenn die Grösse der Partition <16 Elemente: Insertionsort
        * Wenn die Rekursionstiefe von Quicksort >2*log n: Heapsort
        * Andernfalls: Quicksort

## Selbststudium

* Lesen Sie Kapitel 3.1 in Cordts2014
* Bearbeiten Sie das Beispiel in Cordts2014 (Beachten Sie auch die Quellcodes zum Buch – siehe Slides «Einführung»):
    * Rechtschreibprüfung mit binärer Suche (S. 146ff)

* Linear Search
    * https://en.wikipedia.org/wiki/Linear_search
* Binary Search
    * https://en.wikipedia.org/wiki/Binary_search_algorithm

## Searching algorithms

| Algorithm            | Best    | Average  | Worst   | Stabile | Worst-case space complexity |
|----------------------|---------|----------|---------|---------|-----------------------------|
| Linear search        | O(1)    | O(n)     | O(n)    |         | O(1) iterative              |
| Binary search array  | O(1)    | O(log n) | O(log n)|         | O(1)                        |
| Binary search tree   | O(1)    | O(log n) | O(n)    |         |                             |
| Hashing              | O(1)    | O(1)     | O(n)    |         |                             |



### Linear search 
Lineare Suche ist ein Algorithmus, der auch unter dem Namen sequentielle Suche bekannt ist. Er ist der einfachste Suchalgorithmus überhaupt.
Die Aufgabe besteht darin, ein Element in einer Liste oder einem Array mit n Elementen zu finden. Man geht dazu die Liste Element für Element durch, bis man es gefunden hat. Der Suchaufwand wächst linear mit der Anzahl der Elemente in der Liste.
Die effizientere Binäre Suche kann nur bei geordneten Listen benutzt werden.
Für ungeordnete Listen existiert mit Lazy Select noch ein randomisierter Algorithmus, der mit relativ hoher Wahrscheinlichkeit das x-te Element einer Liste bezüglich einer Ordnung schneller als in linearer Zeit finden kann.

![Linear search](Linear-Search-algorithm.png)

### Binary search
Die binäre Suche ist ein Algorithmus, der auf einem Feld (also meist „in einer Liste“) sehr effizient ein gesuchtes Element findet bzw. eine zuverlässige Aussage über das Fehlen dieses Elementes liefert. Voraussetzung ist, dass die Elemente in dem Feld entsprechend einer totalen Ordnungsrelation angeordnet (sortiert) sind. Der Algorithmus basiert auf einer einfachen Form des Schemas „Teile und Herrsche“, zugleich stellt er auch einen Greedy-Algorithmus dar. Ordnung und spätere Suche müssen sich auf denselben Schlüssel beziehen – beispielsweise kann in einem Telefonbuch, das nach Namen geordnet ist, mit binärer Suche nur nach einem bestimmten Namen gesucht werden, nicht jedoch z. B. nach einer bestimmten Telefonnummer. 

![Binary search](Binary_search_into_array.svg)

### Binary search tree 
In der Informatik ist ein binärer Suchbaum eine Kombination der abstrakten Datenstrukturen Suchbaum und Binärbaum. Ein binärer Suchbaum, häufig abgekürzt als BST (von englisch Binary Search Tree), ist ein binärer Baum, bei dem die Knoten „Schlüssel“ tragen, und die Schlüssel des linken Teilbaums eines Knotens nur kleiner (oder gleich) und die des rechten Teilbaums nur größer (oder gleich) als der Schlüssel des Knotens selbst sind.
Was die Begriffe „kleiner gleich“ und „größer gleich“ bedeuten, ist völlig dem Anwender überlassen; sie müssen nur eine Totalordnung (genauer: eine totale Quasiordnung siehe unten) etablieren. Am flexibelsten wird die Ordnungsrelation durch eine vom Anwender zur Verfügung zu stellende 3-Wege-Vergleichsfunktion realisiert. Auch ob es sich um ein einziges Schlüsselfeld oder eine Kombination von Feldern handelt, ist Sache des Anwenders; ferner ob Duplikate (unterschiedliche Elemente, die beim Vergleich aber nicht als „ungleich“ herauskommen) zulässig sein sollen oder nicht. Über Suchfunktionen für diesen Fall siehe unten.
Ein in-order-Durchlauf durch einen binären Suchbaum ist äquivalent zum Wandern durch eine sortierte Liste (bei im Wesentlichen gleichem Laufzeitverhalten). Mit anderen Worten: ein binärer Suchbaum bietet ggf. wesentlich mehr Funktionalität (zum Beispiel Durchlauf in der Gegenrichtung und/oder einen „direkten Zugriff“ mit potentiell logarithmischem Laufzeitverhalten – erzielt durch das Prinzip „Teile und herrsche“, das auf der Fernwirkung des Transitivitätsgesetzes beruht) bei einem gleichen oder nur unwesentlich höheren Speicherbedarf.

![Binary search tree ](Binary-tree-labeled.svg)

### Hashing
In der Informatik bezeichnet man eine spezielle Indexstruktur als Hashtabelle (englisch hash table oder hash map) bzw. Streuwerttabelle. Sie wird verwendet, um Datenelemente in einer großen Datenmenge zu suchen bzw. aufzufinden (Hash- oder Streuspeicherverfahren).
Gegenüber alternativen Index-Datenstrukturen wie Baumstrukturen (z. B. ein B+-Baum) oder Skip-Listen zeichnen sich Hashtabellen üblicherweise durch einen konstanten Zeitaufwand bei Einfüge- bzw. Entfernen-Operationen aus.

![Hashing](Hash_table.svg)


