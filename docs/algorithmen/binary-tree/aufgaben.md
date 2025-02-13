
# Aufgaben Binary Tree

## Wiederholungsaufgaben

### 1. Aufgabe
Was ist das Hauptmerkmal eines Binary Tree? 

* Children - hirachisch
* Jeder Knoten kann maximum 2 Nachkommen haben.

### 2. Aufgabe
Worin unterscheiden sich ein Binary Tree mit einem Binary Search Tree hauptsächlich? 

* Kann sortiert werden (links oder rechts).

* Hat eine bestimmte Systematik.
    * Der Wert jedes Knotens im linken Teilbaum ist kleiner als der Wert des Knotens selbst.
    * Der Wert jedes Knotens im rechten Teilbaum ist größer als der Wert des Knotens selbst.

### 3. Aufgabe
Welche Komplexitätsklasse weisst die Suche in einem Binary Search Tree auf? Begründen Sie.

* Durchschnittliche Zeitkomplexität: O(log n) (bei ausgewogenem Baum) --> balanced
* Schlimmste Zeitkomplexität: O(n) (bei degeneriertem Baum) --> linked List 


### 4. Aufgabe
Worauf muss beim Löschen eines Nodes in einem Binary Search Tree geachtet werden?

* Systematik darf nicht zerstört werden. 
* Der am weitesten Links vom Rechten Nachkommen. ??

* Hauptpunkte die beachtetw werden müssen:
    * Fall 1: Konten ist ein Blatt (keine Kinder) --> kann entfernt werden
    * Fall 2: Konten hat ein Kind --> Knoten entfernen Kind rückt nach
    * Fall 3: Konten hat zwei Kinder --> Nachfolger bestimmen --> kleinster Knoten im rechten Teilbaum, der die Eigenschaften eines Binayr Search Tree beibehält.
    * Nach dem Löschen muss die Anordnung der Knoten weiterhin gültig sein.
    * Bei AVL-Tree müssen weiter Schritte unternommen werden, um den beim ins Gleichgewicht zu bringen

### 5. Aufgabe
Gegeben ist folgende Methode: 

```C#
public int Frage(BinaryTreeNode root) { 
    if (root == null) { 
        return 0; 
    } 
 
    if (root.Left == null && root.Right == null) { 
        return 0; 
    } 
 
    return 1 + Frage(root.Left) + Frage(root.Right); 
}
```
Was berechnet diese Methode? 

* a) Sie zählt die Blattknoten. 
* X b) Sie zählt die internen Knoten. 
* c) Sie berechnet die Höhe des Binärbaumes. 
* d) Etwas anderes – nämlich: ………………………………………………………………… 

### 6. Aufgabe
Gegeben ist folgender Binary Search Tree: 

``` mermaid
flowchart TD
    5 --> 3
    5 --> 9
    3 --> 1
    3 --> 4
    9 --> 7
    7 --> 8
```

Nun werden auf diesem Baum mehrere Baum-Traversierungen durchgeführt und von jedem Knoten die jeweilige 
Zahl auf die Konsole ausgegeben. 
Was ist die jeweilige Ausgabe auf der Konsole für

* Preorder: 5 --> 3 --> 1 --> 4 --> 9 --> 7 --> 8
* Inorder: 1 --> 3 --> 4 --> 5 --> 8 --> 7 --> 9
* Postorder: 1 --> 4 --> 3 --> 8 --> 7 --> 9 --> 5

### 7. Aufgabe:  
a) Bauen Sie einen Binary Search Tree mit folgenden Elementen (in der gegebenen Reihenfolge):  
10, 5, 8, 15, 2, 20. Bestimmen Sie von Ihrem Baum die Komplexitätsklasse für einen Suchvorgang. 

``` mermaid
flowchart TD
    10 --> 5
    10 --> 15
    5 --> 8
    5 --> 2
    15 --> 20
```

* balonzierter Baum --> O(log n)


b) Bauen Sie einen Binary Search Tree mit folgenden Elementen (in der gegebenen Reihenfolge):
20, 15, 10, 5, 2, 8. Bestimmen Sie von Ihrem Baum die Komplexitätsklasse für einen Suchvorgang. 
Was stellen Sie fest, wenn Sie die Komplexitätsklassen vergleichen? Wie könnte dieses Problem gelöst  
werden? 

``` mermaid
flowchart TD
    20 --> 15
    15 --> 10
    10 --> 5
    5 --> 2
    5 --> 8
```

* unbalonzierter Baum --> O(n)

Lösen des Problems durch:

1. Selbstbalancierende Bäume verwenden
2. Rpalancing durchführen
3. Heaps verwenden



!!! note

    n+1  ==> O(n) =  n1 + n0  // ist gleich

## Aufgabe Traversieren 

### 1. Aufgabe

``` mermaid
flowchart TD
    1 --> 2
    1 --> 3
    2 --> 4
    2 --> 5
    4 --> 8
    4 --> 9
    5 --> 10
    5 --> 11
    3 --> 6
    3 --> 7
```

```
          1
        /   \
       2     3
      / \   / \
     4   5 6   7
    / \  / \
   8  9 10 11
```

| Traversieren  | Reihenfolge                           |
| -------       | -----                                 |
| Pre-Order     | 1, 2, 4, 8, 9, 5, 10, 11, 3, 6, 7     |
| In-Order      | 8, 4, 9, 2, 10, 5, 11, 1, 6, 3, 7     |
| Post-Order    | 8, 9, 4, 10, 11, 5, 2, 6, 7, 3, 1     |

### 2. Aufgabe
```
          15
        /    \
      10      20
     /  \    /  \
    8   12  17   25
   / \    \
  6   9   13
```

| Traversieren  | Reihenfolge                           |
| -------       | -----                                 |
| Pre-Order     | 15, 10, 8, 6, 9, 12, 13, 20, 17, 25   |
| In-Order      | 6, 8, 9, 10, 13, 12, 15, 17, 20, 25   | 
| Post-Order    | 6, 9, 8, 13, 12, 10, 17, 25, 20, 15   |


### 3. Aufgabe
Gegebene Traversierungen:

    In-Order: D, B, E, A, F, C
    Pre-Order: A, B, D, E, C, F

```
          A
        /    \
      B       F
     /  \      \ 
    D    E      C
```

### 4. Aufgabe
Gegebene Traversierungen:

    In-Order: 4, 2, 5, 1, 6, 3, 7
    Pre-Order: 1, 2, 4, 5, 3, 6, 7


```
          1
        /    \
      2       3
     /  \    / \ 
    4    5  6   7
```

### 5. Aufgabe

Gegebene Traversierungen:

    In-Order: 8, 4, 9, 2, 10, 5, 1, 12, 6, 3, 14, 7, 11, 15, 13
    Pre-Order: 1, 2, 4, 8, 9, 5, 10, 3, 6, 12, 7, 14, 15, 11, 13

```
          1
        /         \
      2              3
     /  \         /     \ 
    4    5       6       7
   / \    \     /  \ 
  8   9    10  12  11
                \
                 14
                  \
                   15
```

### 6. Aufgabe

```
        A
       / \
      B   C
     / \   \
    D   E   F
       /
      G
```

| Traversieren  | Reihenfolge           |
| -------       | -----                 |
| Pre-Order     | A, B, D, E, G, C, F   |
| In-Order      | D, B, G, E, A, C, F   | 
| Post-Order    | D, G, E, B, F, C, A   |

### 7. Aufgabe

```
                    1
              /         \
             2           3
            / \         / \
           4   5       6   7
          / \  / \    / \  / \
         8  9 10 11 12 13 14 15
```

| Traversieren  | Reihenfolge           |
| -------       | -----                 |
| Pre-Order     | 1, 2, 4, 8, 9, 5, 10, 11, 3, 6, 12, 13, 7, 14, 15   |
| In-Order      | 8, 4, 9, 2, 10, 5, 11, 1, 12, 6, 3, 13, 14, 7, 15   | 
| Post-Order    | 8, 9, 4, 10, 11, 5, 2, 12, 13, 6, 14, 15, 7, 3, 1   |

### 8. Aufgabe
Gegeben sind:

| Traversieren  | Reihenfolge           |
| -------       | -----                 |
| Pre-Order     | 10, 5, 2, 1, 3, 7, 6, 11, 15, 12, 14, 17, 20, 18, 25  |
| In-Order      | 1, 2, 3, 5, 6, 7, 11, 10, 14, 12, 17, 15, 18, 20, 25  | 
| Post-Order    | 1, 3, 2, 5, 6, 11, 7, 5, 14, 17, 12, 18, 25, 20, 15, 10 | 

```
                    10
              /          \
             5             15
            / \          /    \
           2    7       12     20
          / \  / \     / \     / \
         1  3 6  11  14   17  18  25
```

### 9. Aufgabe
Gegeben ist:

```
                    10
              /            \
             5              15
            / \            /    \
           2     7        12     20
          / \    / \     / \     / \
         1   3  6  11   14   17  18  25
                    \           /
                    13         16 
```

| Traversieren  | Reihenfolge           |
| -------       | -----                 |
| Pre-Order     | 10, 5, 2, 1, 3, 7, 6, 11, 13, 15, 12, 14, 17, 20, 18, 16, 25  |
| In-Order      | 1, 2, 3, 5, 6, 7, 11, 13, 10, 14, 12, 17, 15, 16, 18, 20, 25  | 
| Post-Order    | 1, 3, 2, 5, 6, 13, 11, 7, 5, 14, 17, 12, 16, 18, 25, 20, 15, 10 |

https://tree-visualizer.netlify.app/