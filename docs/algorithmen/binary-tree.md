# Binary Tree

## Ziele

* [ ] Ich weiss, was im Allgemeinen ein Binary Tree ist
* [ ] Ich weiss, was im Speziellen ein Binary Search Tree ist
* [ ] Ich kann einen Binary Search Tree grafisch aufbauen
* [ ] Ich kann Elemente suchen und löschen
* [ ] Ich kann den Baum traversieren

## Übersicht

* Baum ist ähnlich wie LinkedList – jedoch nicht linear sondern hierarchisch
* Tree
    * Binary Tree
        * Binary Search Tree
* Hinzufügen und Entfernen
* Suchen
* Traversieren
    * Pre-Order
    * In-Order
    * Post-Order

## Anwendungen

* Speicherung von Hierarchischen Strukturen (Dateisystem, Stücklisten usw.)
* Sortieren (z.B. Heapsort)
* Suchen (Binary Search Tree)
* Partitionierung (k-d Tree)
    * finden aller Objekte in einem 2D oder 3D Fenster (z.B. für Rendering)
    * finden aller Personen, die zwischen 3000 und 4000 verdienen sowie zwischen 1980 und 1990 geboren sind
* Speicherung von Routing-Tables
    * Finden von Routes
* Path-Finding Algorithmen
* Komprimierung von Bilder und Videos (via Clustering)
* Syntax-Tree
* Index einer Datenbank

## Binary Tree
* Hierarchie von Daten
* Ein Root-Node
* 0-2 Childs
    * Left Child
    * Right Child
* Jedes Child ist selber wieder ein Baum

``` mermaid
flowchart TD
    subgraph Level0
        0[Root]
    end
    subgraph Level1
        0 --> 1
        0 --> 2[Inner]
    end
    subgraph Level2
        1 --> 3
        1 --> 4
        2 --> 5
        2 --> 6[Leaf / Blatt]
    end
```

###  Exkurs: Geometrische Reihe
Eine geometrische Reihe ist die Reihe einer geometrischen Folge. Bei einer geometrischen Folge an ist der Quotient r zweier benachbarter Folgenglieder konstant: 
a_(n+1) = a_n(r)

* Ebene 0: Auf der untersten Ebene gibt es nur 1 Node. Das sind 2^0 Nodes.
* Ebene 1: Auf der nächsten Ebene können bis zu 2 Nodes sein. Das sind 2^1 Nodes.
* Ebene 2: Auf der dritten Ebene können bis zu 4 Nodes sein. Das sind 2^2 Nodes.
* …
* Ebene h: Auf der h-ten Ebene können bis zu 2^h Nodes sein.

Maximale Anzahl der Knoten = 2^0+2^1+2^2+⋯+2^h

Die Summe einer solchen geometrischen Reihe ist:

S = a * (1 - r^n) / (1 - r)  für r ≠ 1

S = 1* (1 - 2(h+1)) / (1-2)

Erklärung:
* S: Summe der ersten n Terme
* a: erster Term
* r: gemeinsamer Faktor (Quotient)
* n: Anzahl der Terme


## Binary Search Tree

* Sortierte Hierarchie von Daten
* Ein Root-Node
* Left Child
    * kleiner als Parent
* Right Child
    * grösser als Parent
* Alle Kinder folgen den gleichen Regeln

``` mermaid
flowchart TD
    4 --> 2
    4 --> 6
    2 --> 1
    2 --> 3
    6 --> 5
    6 --> 7
```


## Implementierung

``` mermaid
flowchart TD
    subgraph Datenobjekt
        nextLeft
        nextRight
    end
```

```C#
public class Node
{
    Object object;
    Node nextLeft;
    Node nextRight;
}
```

```C#
public class BinaryTree<T> where T : IComparable<T>
{
    private sealed class Node<TNode> where TNode : IComparable<TNode>
    {
        public TNode Item { get; set; }
        public Node<TNode> Left { get; set; }
        public Node<TNode> Right { get; set; }
        public int CompareTo(TNode other)
        {
            return Item.CompareTo(other);
        }
    }
    private Node<T> root;
…
}
```

### Suchen
```C#
Find(Node current, Data value) {
    if(current == null) {
        return null;
    }
    if(current.Value == value) {
        return current;
    }
    if(value < current.Value) {
        return Find(current.Left, value);
    }
    return Find(current.Right, value);
}
```

``` mermaid
flowchart TD
    4 --> 2
    4 --> 6
    2 --> 1
    2 --> 3
    6 --> 5
    6 --> 7
```

* Find(Root, 3)
* Find(Root, 5)
* Find(Root, 8)

### Löschen

* Suchen des zu löschenden Nodes
    * Wenn er nicht exisitert → exit
* Es handelt sich um einen Leaf-Node
    * Node entfernen
* Es handelt sich um Root- oder Inner-Node
    * Child-Node suchen, mit dem der zu löschende Node ersetzt wird
    * Drei Szenarios …

#### Szenario 1
* Szenario 1: Node hat keinen Right Child
    * Left Child ersetzt gelöschten Node
* Remove(8)
    * Node suchen
    * keinen Right Child
    * Left Child hochziehen

``` mermaid
flowchart TD
    4 --> 2
    4 --> 8
    2 --> 1
    2 --> 3
    8 --> 6
    8 --> 9[?]
    6 --> 5
    6 --> 7
    style 8 fill:#bbf,stroke:#f66,stroke-width:2px,color:#fff,stroke-dasharray: 5 5
```

Remove(8)

``` mermaid
flowchart TD
    4 --> 2
    4 --> 6
    2 --> 1
    2 --> 3
    6 --> 5
    6 --> 7
    style 6 fill:#f9f,stroke:#333,stroke-width:4px
    style 5 fill:#f9f,stroke:#333,stroke-width:4px
    style 7 fill:#f9f,stroke:#333,stroke-width:4px
```

#### Szenario 2
* Szenario 2: Node hat keinen Left Child
    * Right Child ersetzt gelöschten Node
* Remove(6)
    * Node suchen
    * keinen Left Child
    * Right Child hochziehen

``` mermaid
flowchart TD
    4 --> 2
    4 --> 6
    2 --> 1
    2 --> 3
    6 --> ?
    6 --> 7
    7 --> 8
    style 6 fill:#bbf,stroke:#f66,stroke-width:2px,color:#fff,stroke-dasharray: 5 5
```

Remove(6)

``` mermaid
flowchart TD
    4 --> 2
    4 --> 7
    2 --> 1
    2 --> 3
    7 --> ?
    7 --> 8
    style 7 fill:#f9f,stroke:#333,stroke-width:4px
    style 8 fill:#f9f,stroke:#333,stroke-width:4px
```

#### Szenario 3

* Szenario 3: Right Child des gelöschten Nodes hat einen Left Child
    * Most Left Child ersetzt den gelöschten Node
* Remove(6)
    * Node suchen
    * Node hat Left Child
    * Für Right Child den am weitesten links liegenden Child Node suchen
* Diesen Node hochziehen

``` mermaid
flowchart TD
    4 --> 2
    4 --> 6
    2 --> 1
    2 --> 3
    6 --> 5
    6 --> 8
    8 --> 7
    style 7 fill:#bbf,stroke:#f66,stroke-width:2px,color:#fff,stroke-dasharray: 5 5
```

Remove(6)

``` mermaid
flowchart TD
    4 --> 2
    4 --> 7
    2 --> 1
    2 --> 3
    7 --> 5
    7 --> 8
    style 7 fill:#f9f,stroke:#333,stroke-width:4px
```

### Traversieren
* Nodes werden in einer definierte Reihenfolge iteriert / Ausgabe als Text
* Drei verschiedene Algorithmen
* Grundlegender Algorithmus
    * Bearbeite aktuellen Node
    * Besuche Left Child
    * Besuche Right Child
* Die Reihenfolge wird nun variiert
    * Pre-Order
    * In-Order
    * Post-Order

#### Pre-Order
Node → links → rechts

```C#
Visit(Node current) {
    if(current == null) {
        return;
    }
    Process(current.Value);
    Visit(current.Left);
    Visit(current.Right);
}
```

5 → 3 → 2 → 4 → 8 → 7 → 9

``` mermaid
flowchart TD
    5 --> 3
    5 --> 8
    3 --> 2
    3 --> 4
    8 --> 7
    8 --> 9
```

#### Post-Order
links → rechts → Node

```C#
Visit(Node current) {
    if(current == null) {
        return;
    }
    Visit(current.Left);
    Visit(current.Right);
    Process(current.Value);
}
```

2 → 4 → 3 → 7 → 9 → 8 → 5

``` mermaid
flowchart TD
    5 --> 3
    5 --> 8
    3 --> 2
    3 --> 4
    8 --> 7
    8 --> 9
```

#### In-Order

links → Node → rechts

```C#
Visit(Node current) {
    if(current == null) {
        return;
    }
    Visit(current.Left);
    Process(current.Value);
    Visit(current.Right);
}
```

2 → 3 → 4 → 5 → 7 → 8 → 9

``` mermaid
flowchart TD
    5 --> 3
    5 --> 8
    3 --> 2
    3 --> 4
    8 --> 7
    8 --> 9
```

## Aufgabe
* Implementieren Sie in der Klasse BinaryTree<T> (siehe BinaryTreeDemo auf Moodle) die Methode Traverse() gemäss den vorgängigen Definitionen.
    * Den gewünschten Mode können Sie aus dem Property TraverseMode lesen

```C#
private string Traverse() {
    var s = "";
    var level = 0;

    Traverse(root, level, ref s);
    return s;
}

private void Traverse(Node<T> node, int level, ref string s) {
    if (node == null) {
        return;
    }

    var reverse = TraverseMode == TraverseModeEnum.ReverseInOrder;
    
    if (TraverseMode == TraverseModeEnum.PreOrder) {
        s += "".PadLeft(level, ' ') + node.Item + "\n";
    }

    Traverse(reverse ? node.Right : node.Left, level + 2, ref s);
    
    if (TraverseMode == TraverseModeEnum.InOrder || TraverseMode == TraverseModeEnum.ReverseInOrder) {
        s += "".PadLeft(level, ' ') + node.Item + "\n";
    }

    Traverse(reverse ? node.Left : node.Right, level + 2, ref s);
    
    if (TraverseMode == TraverseModeEnum.PostOrder) {
        s += "".PadLeft(level, ' ') + node.Item + "\n";
    }
}
```

### Balancierung 

* Erstellen Sie einen Binary Search Tree mit folgenden Werten (die Werte sollen in dieser Reihenfolgen eingefügt werden): 
140, 150, 130, 110, 135, 160
* Erstellen Sie anschliessend einen Baum mit den Werten in folgender Reihenfolge:
110, 130, 135, 140, 150, 160
* Was stellen Sie fest?

#### Balancierter Baum
``` mermaid
flowchart TD
    140 --> 130
    140 --> 150
    130 --> 110
    130 --> 135
```
#### Nicht Balancierter Baum
``` mermaid
flowchart TD
    110 --> 130 --> 135 --> 140 --> 150 --> 160
```

* Ziel eines Baumes: weitgehend balanciert
* Binärer Baum berücksichtigt die Balancierung nicht
* Worst-Case: Suche O(n) – wenn der Baum zu Liste entartet!
* Im vollständig balancierten Baum:
    O(h) – wobei h = Höhe des Baumes, ℎ ≥ 𝑙𝑜𝑔2(𝑛 + 1)
* Balancierte Bäume müssen ggf. reorganisiert werden:

``` mermaid
flowchart TD
    7 --> 3
    7 --> 11
    3 --> 1
    3 --> 5
    1 --> 2
    5 --> 4
    5 --> 6
    11 --> 9
    11 --> 13
    9 --> 8
    9 --> 10
    13 --> 12
    13 --> 14
```

* Hinzufügen von +15

``` mermaid
flowchart TD
    8 --> 4
    8 --> 12
    4 --> 2
    4 --> 6
    2 --> 1
    2 --> 3
    6 --> 5
    6 --> 7
    12 --> 10
    12 --> 14
    10 --> 9
    10 --> 11
    14 --> 13
    14 --> 15
```

* AVL-Tree, B-Tree, Red-Black-Tree

## Selbststudium
* Lesen Sie Kapitel 2.6 in Cordts2023, Lösen Sie die Aufgaben zum Kapitel
* Bearbeiten Sie das Beispiel in Cordts2023 (Beachten Sie auch die Quellcodes zum Buch – siehe Slides «Einführung»):
    * Suchen nach Firmenbezeichnungen (S. 120ff)
* https://www.cs.usfca.edu/~galles/visualization/BST.html
    * Achtung: Diese Visualisierung verwendet eine leicht andere Regel für Szenario 3 beim Löschen.
    * Szenario 3 lautet: Node hat zwei Childs. Suche für Left-Child den am weitesten rechts liegende Node. Dieser ersetzt den gelöschten Node.