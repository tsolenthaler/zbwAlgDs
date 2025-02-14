# AVL Tree

## Ziele

- [ ] Ich kennen den Unterschied zwischen einem unbalanced und balanced Tree
- [ ] Ich weiss, was ein AVLTree ist und verstehen seinen Balancing-Algorithmus
- [ ] Ich kann einen AVLTree implementieren

## Übersicht

* Self-balancing Binary-Search-Tree erfunden von Adelson-Velsky & Landis 1962 (russische Mathematiker) – älteste Datenstruktur für balancierte Bäume
* Ähnlich wie Binary Search Trees
    * Gleiche strukturelle Regeln
    * Suche und Iteration/Traversierung ist identisch
    * Einfügen und Löschen unterscheidet sich «nur» dadurch, dass zusätzlich ein Balance-Algorithmus angewendet wird (wenn nötig)
* Neue Konzepte 
    * Self-Balancing
    * Höhe
    * Balance Faktor
    * Rechts/Links lastig

## Balanced

### Balanced Binary Search Tree

* Der Baum bleibt balanciert, wenn Nodes eingefügt und gelöscht werden
    * O(log n) für Suche
* Für jeden Knoten gilt: Höhe des Left Childs weicht von der des Right Childs höchstens ±1 ab
* Beispiel
    * Einfügen der Werte 1, 2, 3, 4

``` mermaid
flowchart TD
    2 --> 1
    2 --> 3
    3 --> 4
```

### Balanced Einfügen und Löschen

* Einfügen ist identisch wie beim Binary Search Tree
    * Kleinerer Wert links
    * Grösserer oder gleicher Wert rechts
* Löschen ist identisch wie beim Binary Search Tree
    * Der zu löschende Node wird gesucht
    * Child-Nodes werden bezogen auf die drei Regeln verschoben
* Nach dem Einfügen und dem Löschen eines Nodes wird für jeden Parent-Node des gesamten Trees der Balance-Algorithmus ausgeführt

## Implementierung

* Klasse AVLTree entspricht fast der Klasse BinaryTree
    * Ausnahme: Beim Einfügen und Löschen wird der Balance-Algorithmus ausgeführt
* Klasse Node beinhaltet Funktionalität für Self-Balancing

## Balacing Algorithmus
* Für Balacing wird «Node-Rotation» verwendet
* Rotation wird beim Einfügen und Löschen ausgeführt
    * für den betreffenden Node und seine Parents
* Rotation ändert die physikalische Struktur des Trees damit diese wieder den Anforderungen eines Binary Search Trees entsprechen
* Rotation Algorithmen
    * Right Rotation
    * Left Rotation
    * Right-Left Rotation
    * Left-Right Rotation

## Welche Rotation?

* Tree rechts lastig
    * Wenn Right Child links lastig
        * Right-Left Rotation
    * Sonst
        * Left Rotation
* Tree links lastig
    * Wenn Left Child rechts lastig
        * Left-Right Rotation
    * Sonst
        * Right Rotation

```C#
internal void Balance() {
    if (State == TreeState.RightHeavy) {
        if (Right != null && Right.BalanceFactor < 0) {
            RightLeftRotation();
        } else {
            LeftRotation();
        }
    } else if (State == TreeState.LeftHeavy) {
        if (Left != null && Left.BalanceFactor > 0) {
            LeftRightRotation();
        } else {
            RightRotation();
        }
    }
}
```

### Right Rotation

* Algorithmus dreht einen Node nach rechts
    * Left Child wird neuer Root-Node
    * Right Child des neuen Root-Nodes wird Left Child des alten Root-Nodes
    * Alter Root-Node wird Right Child des neuen Root-Nodes
* Beispiel – Rotation nachdem «1» eingefügt wurde
    * Rechte Höhe von Node «4» ist 0
    * Linke Höhe von Node «4» ist 2
    * «2» wird neuer Root-Node
    * «4» wird Right Child von «2»
    * «3» wird Left Child von «4»


* Baum ist links-lastig --> Right Rotation
```
       4
      /
     2
    / \
   1  3
```

* 4 wird Right Child von 2

```
     2   4
    / \
   1  3
```

* 3 wird Left Child von 4
```
     2   4
    /   /
   1   3
```

* 4 wird Right Child von 2
```
     2
    / \
   1   4
      /
     3
```

### Left Rotation
* Algorithmus dreht einen Node nach links
    * Right Child wird neuer Root-Node
    * Left Child des neuen Root-Nodes wird Right Child des alten Root-Nodes
    * Alter Root-Node wird Left Child des neuen Root-Nodes
* Beispiel – Rotation nachdem «4» eingefügt wurde
    * Linke Höhe von Node «1» ist 0
    * Linke Höhe von Node «1» ist 2
    * «3» wird neuer Root-Node
    * «2» wird Right Child von «1»
    * «1» wird Left Child von «3»


* Baum ist rechts-lastig --> left Rotation
```
     1
      \
       3
      / \
     2   4
```

* 1 wird Linke Höhe von Node 1 ist 0
* 3 Wird neuer Root-Node
```
   1   3
      / \
     2   4
```

* 2 wird Right Child von 1
```
   1   3
    \   \
     2   4
```

* 1 wird Left Child von 3
```
       3
     /  \
    1    4
     \
      2
```


### Left-Right Rotation
* Right Rotation kann wiederum in einen unbalanced Tree resultieren
* Lösung
    * Left Rotation des Left Child
    * Right Rotation des aktualisierten Trees
* Beispiel
    * Left Rotation von «1»
    * Right Rotation von «3»


* Right Rotation dreht diesen Baum wieder ins unbalanced!
```
       3
     / 
    1    
     \
      2
```
* Nach Right Rotation
```
      1
       \
        3 
       /
      2
```

* Lösung --> Left Rotation und Right Rotation = Left-Right Rotation
* Beispiel
    * Left Rotation 1
    * Right Rotation 3

1. Select 1
```
       3
     / 
    1    
     \
      2
```
2. Left Rotation von 1
```
       3
     / 
    2    
   /
  1
```
3. Right Rotation von 3
```
    2    
   / \
  1   3
```


### Right-Left Rotation

* Left Rotation kann wiederum in einen unbalanced Tree resultieren
* Lösung
    * Right Rotation des Right Child
    * Left Rotation des aktualisierten Trees
* Beispiel
    * Right Rotation von «3»
    * Left Rotation von «1»

``` mermaid
flowchart TD
    2 --> 1
    2 --> 3
```

## Vom Binary-Tree zum AVL-Tree

!!! info

    AVL-Tree entspricht einem Binary Tree, welcher nach Add() sowie Remove() neu balanciert

## AVLTreeView

* Demo
* Verwendet «Microsoft Automatic Graph Layout» - diese Lib ist in der Lage, Graphen zu zeichnen 

https://github.com/Microsoft/automatic-graph-layout

https://en.wikipedia.org/wiki/Microsoft_Automatic_Graph_Layout

## Selbststudium
* AVLTree
    * https://en.wikipedia.org/wiki/AVL_tree
    * https://www.cs.usfca.edu/~galles/visualization/AVLtree.html
* Tree Rotation
    * https://en.wikipedia.org/wiki/Tree_rotation
* Binary Tree
    * https://en.wikipedia.org/wiki/Binary_tree


## Aufgaben

### Aufgabe 1
Entwickeln Sie den entstehenden AVLTree zeichnerisch. Alle durchzuführenden Rotationen sollen sichtbar sein. D.h. zeichnen Sie den Baum jeweils vor und nach der Rotation (inkl. Teilrotationen) auf.

70, 77, 65, 85, 83, 63, 61, 81, 82, 80, 73, 72, 75, 60

### Aufgabe 2

Analog Aufgabe 1 jedoch mit folgenden Daten:

67, 6, 4, 80, 55, 40, 58, 48, 2, 50, 36, 49

### Aufgabe 3

In folgendem AVLTree sollen der Reihe nach, folgende Elemente gelöscht werden:

4, 8, 6, 5, 2, 1, 7, 3, 10

Zeichnen Sie den Baum nach jeder Löschoperation neu auf.

``` mermaid
flowchart TD
    5 --> 3
    5 --> 8
    3 --> 2
    3 --> 4
    2 --> 1
    8 --> 7
    8 --> 10
    7 --> 6
    10 --> 9
    10 --> 11
```