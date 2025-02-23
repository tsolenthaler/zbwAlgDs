# B-Tree

## Ziele

- [ ] Ich kenne den Unterschied zwischen einem BinaryTree und einem B-Tree
- [ ] Ich weiss, wie die Operationen «Einfügen» und «Löschen» auf einen B-Tree angewendet werden

## Motivation

Die Verwendung von AVL-Trees für die Indexierung der Datenbank könnte zwar eine ausgeglichene Baumstruktur und effiziente Suchoperationen in Theorie gewährleisten, aber bei jeder Einfügung oder Löschung von Daten müssten möglicherweise mehrere Rotationen durchgeführt werden, um den Baum auszugleichen. Dies ist insbesondere problematisch, wenn die Datenbank auf einem Festplattenspeicher liegt, da jede Änderung im Baum zu potenziell vielen Plattenzugriffen führen kann, um die betroffenen Knoten zu lesen oder zu schreiben. Da Plattenzugriffe im Vergleich zu Operationen im Arbeitsspeicher sehr langsam sind, könnten die Wartungskosten des AVL-Trees in einer solchen Umgebung sehr hoch werden.

## Übersicht

* Erfunden von Rudolf Bayer und Edward M. McCreight 1972 für die Verwaltung von Indizes in relationalen Datenbanken (erfunden von Edgar F. Codd 1970)
* Keine Erklärung für Herkunft des Namens. Interpretation: B für balanciert, Bayer, Barbara (Frau von Bayer), Boeing (Bayer arbeitete für Boeing Scientific Research)
* kleiner als ">1" 1 Key pro Node
* ≥ 2 Child Nodes
* Self-Balancing
* Grössere Verzweigungsgrad reduziert die Baumhöhe und somit die Anzahl Lesezugriffe
* Variable Schlüsselmenge pro Node vermeidet häufiges Balancing

## Eigenschaften
* Jede Page enthält höchstens 2𝑑 Keys (Elemente)
* Jede Page, ausser Root, enthält mindestens 𝑑 Keys
* Root hat min. 1 und max. 2𝑑 Keys
* Jede Page ist entweder Leaf, d.h. hat keine Childs oder sie hat 𝑚 + 1 Childs, wobei 𝑚 die Anzahl ihrer Keys ist
* Die Keys einer Page sind aufsteigend sortiert
* Alle Leafs liegen auf der gleichen Stufe
* Wie bei Binary Search Tree: Links → kleiner, rechts → grösser oder gleich

``` mermaid
flowchart TD
    1[34]
    1 --> 2[12 29]
    1 --> 3[46 67]
    2 --> 4[2 8 9 10]
    2 --> 5[15 19 22 24]
    2 --> 6[30 31 32]
    3 --> 7[36 39]
    3 --> 8[53 57 63 65]
    3 --> 9[72 83 94 96]
```

## Aufgabe

* Berechnen Sie die max. Anzahl Keys, die in einem Baum 2. Ordnung (d.h. d=2) und h=3 gespeichert werden können.
* Tipp: Überlegen Sie sich, wieviele Keys in einem BinaryTree gespeichert werden können und versuchen Sie, Ihre Überlegungen zum oben spezifizierten B-Trees zu transferieren.

## Einfügen

* Keys werden immer in Leafs eingefügt
* Beispiel (𝑑 = 2):

``` mermaid
flowchart TD
    A[32]
    A --> B[9 12 23 27]
    A --> C[33 45 54 67]
```

Einfügen 36

``` mermaid
flowchart TD
    A[32 45]
    A --> B[9 12 23 27]
    A --> C[33 36]
    A --> D[54 67]
```


* 36 wird in Page C eingefügt: (33,36,45,54,67) → Overflow
* Der Node wird aufgeteilt und das mittlere Element (45) nach oben gezogen
* Nun muss Page A bzgl. Overflow geprüft werden → i.O.


## Löschen
* zwei Fälle
    * Das zu löschende Element liegt auf Leaf → trivial
    * Element liegt nicht auf Leaf – das zu löschende Element wird durch das nächstgrössere (nächstkleinere) Element ersetzt. Dieses liegt immer auf Leaf (Suche analog BinarySearchTree)
* Beide Fälle erfordern eine Prüfung der Regel: min. 𝑑 Elemente Enthält die Page P durch Entfernen weniger als d Elemente, so werden die Elemente der Page P und der benachbarten Page Q gleichmässig auf beide Pages verteilt (ausbalanciert)

``` mermaid
flowchart TD
    A[32 45]
    A --> B[9 12 23]
    A --> C[33 36]
    A --> D[54 67 86]
```

Element 36 löschen

``` mermaid
flowchart TD
    A[32 54]
    A --> B[9 12 23]
    A --> C[33 45]
    A --> D[67 86]
```

* Wenn kein Element zum Angliedern vorhanden (d.h. P und Q enthalten 2𝑑 − 1 Elemente)
    * Page P und Q werden zusammengelegt und Element wird von Parent runtergezogen (Gegenteil von Einfügen)

``` mermaid
flowchart TD
    A[32 54]
    A --> B[9 12 23]
    A --> C[33 45]
    A --> D[67 86]
```

Element 45 löschen

``` mermaid
flowchart TD
    A[32]
    A --> B[9 12 23]
    A --> C[33 54 67 86]
```


* Das runterziehen kann die Grösse ebenfalls unter d sinken lassen
    * gleiche Aktion wird für diese Page wiederholt
    * kann sich bis zum Root fortsetzen


## Selbststudium

* B-Tree
    * https://en.wikipedia.org/wiki/B-tree
        * Wichtig: die englische Variante verwenden – die deutsche Variante verwendet eine andere Definition des B-Tree’s

### Hilfe

[B-Tree](https://studyflix.de/informatik/b-baum-1435)


### Unterschied

* Binärbaum: Jeder Knoten hat maximal zwei Kinder, kann unterschiedliche Strukturen haben und ist oft einfacher, aber weniger effizient bei großen Datenmengen.

* B-Baum: Jeder Knoten kann mehrere Schlüssel und Kinder haben, ist selbstbalancierend und optimiert für die Speicherung und den Zugriff auf große Datenmengen, insbesondere in externen Speichersystemen