# B-Tree

## Ziele

* Ich kenne den Unterschied zwischen einem BinaryTree und einem B-Tree
* Ich weiss, wie die Operationen «Einfügen» und «Löschen» auf einen B-Tree angewendet werden

## Motivation

Die Verwendung von AVL-Trees für die Indexierung der Datenbank könnte zwar eine ausgeglichene Baumstruktur und effiziente Suchoperationen in Theorie gewährleisten, aber bei jeder Einfügung oder Löschung von Daten müssten möglicherweise mehrere Rotationen durchgeführt werden, um den Baum auszugleichen. Dies ist insbesondere problematisch, wenn die Datenbank auf einem Festplattenspeicher liegt, da jede Änderung im Baum zu potenziell vielen Plattenzugriffen führen kann, um die betroffenen Knoten zu lesen oder zu schreiben. Da Plattenzugriffe im Vergleich zu Operationen im Arbeitsspeicher sehr langsam sind, könnten die Wartungskosten des AVL-Trees in einer solchen Umgebung sehr hoch werden.

## Übersicht

* Erfunden von Rudolf Bayer und Edward M. McCreight 1972 für die Verwaltung von Indizes in relationalen Datenbanken (erfunden von Edgar F. Codd 1970)
* Keine Erklärung für Herkunft des Namens. Interpretation: B für balanciert, Bayer, Barbara (Frau von Bayer), Boeing (Bayer arbeitete für Boeing Scientific Research)
* >1 Key pro Node
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
    2 --> 1
    2 --> 3
    3 --> 4
```