# Heap Priorityqueue

## Ziele

- [ ] Ich kennen den Unterschied zwischen einem BinarySearchTree und einem Heap
- [ ] Ich kennen die grundlegenden Operationen eines Heaps
- [ ] Ich kennen mögliche Anwendungen eines Heaps


### Motivation

* Kontext: Planung von Flugrouten
    * Eine Fluggesellschaft muss täglich hunderte von Flügen planen und durchführen. Jeder Flug hat verschiedene Attribute, die seine Priorität beeinflussen können, wie z.B. die Flugzeit, die Anzahl der Passagiere, Wetterbedingungen und die strategische Bedeutung bestimmter Routen für das Netzwerk der Fluggesellschaft.
    * Es ist essentiell, dass die Fluggesellschaft in der Lage ist, ihre Ressourcen
    (Flugzeuge, Crews) effizient einzusetzen, um maximale Effizienz und Kundenzufriedenheit zu erreichen.

* Problemstellung: Effiziente Ressourcennutzung und Priorisierung
    * Das Kernproblem besteht darin, eine effiziente Reihenfolge für die Durchführung der Flüge zu finden, sodass:
    * Flüge mit höherer Priorität (z.B. Langstreckenflüge, Flüge mit vielen Passagieren, Flüge in Gebiete mit günstigen Wetterfenstern) vorrangig behandelt werden.
    * Ressourcen (Flugzeuge und Besatzungen) optimal genutzt werden, um Verspätungen zu minimieren und den Betrieb unter verschiedenen Umständen aufrechtzuerhalten.

* Häufig ist das Prinzip einer einfachen Warteschlange (Queue) nicht ausreichend
* Es sollen Elemente bevorzugt werden können
    * Planung von Flugrouten (Reihenfolge der Landung)
    * behinderte Personen
    * Prozessmanagement im Betriebssystem
    * Notfälle im Wartezimmer
* Lösung: die Elemente in einer Queue werden mit Prioritäten versehen
* Priorityqueue: Elemente werden in Abhängigkeit ihrer Priorität und ihrer Position aus der Warteschlange entnommen

### Realisierung

* Intuitiv
    * Prioritätswarteschlangen können ebenfalls mit Hilfe von Listen implementiert werden.
    * Wir unterscheiden hierbei zwei Varianten:
        1. Verwendung einer Schlangen-Datenstruktur mit Einfügen neuer Elemente am Ende der Liste.
        2. Geordnetes Einfügen neuer Elemente in die Liste gemäß ihrer Priorität.

* Nachteil Variante 1
    * Die Entnahme (dequeue) des Elements mit der höchsten Priorität läuft in O(n), da dieses Element erst gesucht werden muss.

* Nachteil Variante 2
    * Das Einfügen (enqueue) eines Elements gemäß seiner Priorität läuft in O(n), da die Einfügeposition nur durch sequentielles Durchlaufen der Liste bestimmt werden kann.

### Optimierung: Heap (als Datenstruktur für Prioritätswarteschlangen)

* Definition
    * Ein Heap ist eine besondere Form eines binären Baums und es gilt, dass
        * der Wert eines Nodes in einer Ordnungsrelation zu den Werten seiner Childs steht
    * er perfekt balanciert ist und die Leafs der letzten Ebene linksbündig vollständig sind
* Ordnungsrelation
    * In Abhängigkeit der Beziehung zwischen einem Node und seinen Childs unterscheiden wir zwei Heapvarianten:
        * MinHeap - Der Wert eines Nodes ist kleiner oder gleich den Werten seiner Childs.
        * MaxHeap - Der Wert eines Nodes ist größer oder gleich den Werten seiner Childs.

#### Beispiel MaxHeap

#### Werte

``` mermaid
flowchart TD
    1[89] --> 2[72]
    1 --> 3[18]
    2 --> 4[43]
    2 --> 5[49]
    3 --> 6[15]
    3 --> 7[3]
    4 --> 8[39]
```

#### Positionen / Index

``` mermaid
flowchart TD
    1 --> 2
    1 --> 3
    2 --> 4
    2 --> 5
    3 --> 6
    3 --> 7
    4 --> 8
```

### Implementierung

* Konsequenz der Heap-Definition
    * Alle Leafs befinden sich auf den letzten beiden Ebenen und bis auf die letzte Ebene sind alle Ebenen vollständig gefüllt, d.h. jede innere Ebene enthält doppelt so viele Elemente wie die Vorgängerebene. Des Weiteren befinden sich keine „Lücken“ zwischen den Leafs der letzten Ebene. Auf diesem Grund können Heaps mit Hilfe von Arrays dargestellt werden.
* Darstellung als Array
    * Die Parent-Child-Beziehung eines MaxHeaps in einem Array maxHeap der Länge 𝑁 kann wie folgt definiert werden:
        * maxHeap[i] ≥ maxHeap[2*i+1] --> für 0 ≤ i < (N–1) / 2 --> (Relation zu linkem Kind)
        * maxHeap[i] ≥ maxHeap[2*i+2] --> für 0 ≤ i < (N–2) / 2 --> (Relation zu rechtem Kind)
* Konsequenz für Operationen
    * Wir beschränken und aufgrund der Anwendungsbereiche neben dem Lesen des Root-Elements auf das Einfügen eines neuen Elements in einen Heap(heapEnqueue) und das Entfernen des Root-Elements (heapDequeue)

####  Beispiel MaxHeap als Array

| 1         |  2      | 3   | 4     | 5     | 6     | 7    | 8    |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- |
| 89        | 72      | 18      | 43      | 49      | 15       | 3     | 39     |

### heapEnqueue 🔴

1. Einfügen eines Elements
    * Um ein Element 𝑒 einem Heap hinzuzufügen, fügen wir 𝑒 als letztes Leaf hinzu (d.h. am Ende des Arrays)
2. Rekonstruktion der Heap-Eigenschaft
    * Nach dem Einfügen von 𝑒 ist in der Regel die Heap-Eigenschaft verletzt
    * Diese wird wiederhergestellt, in dem 𝑒 gemäss derOrdnungsrelation solange mit seinem jeweiligen Parent-Node vertauscht wird, bis sich 𝑒 an der richtigen Position im Heap befindet

### heapDequeue 🔴

* Prinzip
    * Entfernen des Root-Node und ersetzen durch den letzten Leaf-Node
    * Wiederherstellung der Heap-Eigenschaft, indem das neue Root solange abwärts in Richtung Leaf-Level verschoben wird, bis sich dasElement gemäss Ordnungsrelation an der richtigen Position befindet
    * Beim «abwärts schieben» stehen zwei Child-Nodes zur Auswahl:
        * Auswahlstrategie bei MinHeap:
        Ist der abwärts zu verschiebende Node grösser als beide Child-Nodes, dann vertausche ihn mit dem kleineren Child (das danach als Parent-Node des grösseren Childs fungiert)
        * Auswahlstrategie bei MaxHeap:
        Ist der abwärts zu verschiebende Node kleiner als beide Child-Nodes, dann vertausche ihn mit dem grösseren Child (das danach als Parent-Node des kleineren Childs fungiert)

### Verwendung von Heaps

* Heaps als Prioritätswarteschlangen (Priorityqueue’s)
    * Mit Heaps lassen sich Prioritätswarteschlangen effizient realisieren, da sich das Element mit dem höchsten Wert (der höchsten Priorität) automatisch in der Wurzel eines MaxHeaps befinden würde
* Komplexität
    * Da Heaps perfekt balanciert sind, lässt sich ein Blatt von der Wurzel aus in O(log n) Schritten erreichen.
    * Entnehmen der Wurzel aus Heap (= dequeue der Prioritätswarteschlange) benötigt maximal O(log n) Schritte um die Heapeigenschaft zu rekonstruieren.
    * Einfügen eines Elements in den Heap (= enqueue der Prioritätswarteschlange) benötigt maximal O(log n) Schritte um die Heapeigenschaft zu rekonstruieren.
* Konsequenz:
    * Die zwei wesentlichen Operationen der Prioritätswarteschlange laufen in O(log n)


* Heaps sind geeignet
    * für das schnelle Auffinden in O(1) des Minimums (MinHeap) oder Maximums (MaxHeap)
    * für das schnelle Entnehmen der Wurzel und das schnelle Einfügen eines neuen Knotens in den Heap, da beide Operationen in O(log n) laufen (Worst Case)
* Heaps sind nicht geeignet
    * für das Auffinden beliebiger Elemente im Baum, da Komplexität O(n)
* Heapsort (wird bei den Sortieralgorithmen behandelt)

## Selbststudium
* Heap
    * https://en.wikipedia.org/wiki/Heap_(data_structure)
* Priorityqueue
    * https://en.wikipedia.org/wiki/Priority_queue


### Hilfe

[Hilfe](https://studyflix.de/informatik/heap-1440)

### Regel

* Von Oben nach Unten
* Von Link nach Rechts


#### Mini-HEAP
* Eltern-Knoten immer kleiner oder gleich des Kindsknoten ist.

```
            2
        /       \
      6          9
    /  \       /  \
   12  15     18   23
``` 
#### Einfügen von 26
```
            2
        /       \
      6          9
    /  \       /  \
   12  15     18   23
  /
 26
``` 
#### Einfügen von 12
```
            2
        /       \
      6          9
    /  \       /  \
   12  15     18   23
  / \
 26  10
``` 

* Heap-Bedingung verletzt --> 12 grösser als 10 
* tauschen von 10 und 12

```
            2
        /       \
      6          9
    /  \       /  \
   10  15     18   23
  / \
 26  12
``` 
#### Einfügen von 3
```
            2
        /       \
      6             9
    /    \        /  \
   10     15     18   23
  / \     /
 26  12  3
``` 

* Heap-Bedingung verletzt --> 3 kleiner als 15 
* tauschen mit 3 mit 15
* und tauschen 3 mit 6

```
            2
        /       \
      3             9
    /    \        /  \
   10     6     18   23
  / \     /
 26  12  15
``` 

#### Max-HEAP
* Umgekehrt von min-Heap
* Die Werte im Kinds-Knoten müssen kleiner oder gleich des Eltern-Knoten sein.

```
            60
        /       \
      45          55
    /    \       
   25     30 
``` 

#### Löschvorgang
```
            2
        /       \
      6             9
    /    \        /  \
   10     15     18   23
  / \    
 12  26 
``` 
##### Löschen von 2 - Einfügen in Speicher
```
            
        /       \
      6             9
    /    \        /  \
   10     15     18   23
  / \    
 12  26 
``` 

* verwenden des letzten Elements im Hepa --> 26

```
            26
        /       \
      6             9
    /    \        /  \
   10     15     18   23
  /    
 12  
``` 

* tauschen mit kleineren Kindknoten

```
            6
        /       \
      10             9
    /    \        /  \
   12     15     18   23
  /    
 26  
``` 
##### Löschen von 23 - Einfügen in Speicher
```
            6
        /       \
      10            9
    /    \        /  \
   12     15     18   
  /    
 26  
``` 

* Baum muss von oben nach unten und von links nach rechts aufgebaut werden
    * 3 Ebene wieder aufüllen

```
            6
        /       \
      10            9
    /    \        /  \
   12     15     18   26 
``` 

#### Heap als Array

##### Formel
``` 
        n
    /     \
2x0+1     2x0+2
``` 

##### Baum
```
            2
        /       \
      6             9
    /    \        /  \
   10     15     18   23
  / \    
 12  26 
``` 


##### Tabelle
| Element       |  2     | 6   | 9     | 10    | 15   | 18   | 23   | 12   | 26   |
| -------       | -----  | --- | ----- | ----- | ---- | ---- | ---- | ---- | ---- |
| Speicherzelle | 0      | 1   | 2     | 3     | 4    | 5    | 6    | 7    | 8    |


## Aufgaben 🔴

### 1. Aufgabe 🔴
In einem Heap befinden sich die Childs eines Nodes mit dem Index X an den Positionen X+1 und X+2. Richtig oder Falsch? Begründen Sie. 

--> Falsch. In einem Heap sind die Child-Nodes nicht beim Position X+1 und X+2.

Sondern:
* (2 * X) + 1
* (2 * X) + 2

### 2. Aufgabe 🔴
Auf der heap-basierenden Priorityqueue pq (realisiert durch einen MinHeap) wird die folgende Sequenz 
von Operationen ausgeführt: 

```C#
pq.Add(8); 
pq.Add(6); 
pq.Add(7); 
pq.Add(5); 
pq.Add(5); 
pq.Add(8); 
var min = pq.Pop();
```
 
Es soll im Folgenden der Heap nach jeweils jeder Operation aufgezeichnet werden:

``` mermaid
flowchart TD
    5 --> 6
    5 --> 7
    6 --> 8
```

Array:
* 5 6 7 8

1. Nach Add(8): [8]
2. Nach Add(6): [6, 8]
3. Nach Add(7): [6, 8, 7]
4. Nach Add(5): [5, 6, 7, 8]
5. Nach Add(5): [5, 5, 7, 8, 6]
6. Nach Add(8): [5, 5, 7, 8, 6, 8]
7. Nach Pop(): [5, 6, 7, 8]

* minHeap - Der Wert eines Nodes ist kleiner oder gleich den Werten seiner Childs.

### 3. Aufgabe 🔴
Gegeben ist nachfolgendes, korrekt funktionierendes Code-Fragment einer Listen-Klasse:$

```C#
public class List { 
    private class Node { 
        public int Key; 
        public Node Next; 
    } 
 
    private Node head;   // points to the first node of the list. 
    private Node tail;   // points to the last node of the list. 
 
    // ... more code (insert-method, etc.) 
 
    public bool ContainsKey(int key) { 
        if (this.head == null) { 
            return false; 
        } 
 
        if (this.head.Key == key) { 
            return true; 
        } 
 
        if (this.head == this.tail) { 
            return false; 
        } 
 
        Node node = this.head; 
        do { 
            node = node.Next; 
            if (node.Key == key) { 
                return true; 
            } 
        } while (node != tail); 
 
        return false; 
    } 
}
```
 
Es soll nun die Methode ContainsKeySentinel erstellt werden, welche von aussen gesehen gleich funktioniert wie ContainsKey, aber unter Anwendung eines Sentinels. Dabei darf der Klasse keine weiteren Attribute oder Methoden hinzugefügt werden.

```C#
public bool ContainsKeySentinel(int key) {
    // Erstellen eines Sentinel-Knotens
    Node sentinel = new Node { Key = int.MinValue, Next = null };

    // Wenn die Liste leer ist, gibt es keinen Schlüssel
    if (this.head == null) {
        return false;
    }

    // Verknüpfen des Sentinel-Knotens am Ende der Liste
    Node current = this.head;
    while (current.Next != null) {
        current = current.Next;
    }
    current.Next = sentinel; // Sentinel am Ende der Liste hinzufügen

    // Durchlaufen der Liste bis zum Sentinel
    Node node = this.head;
    while (node.Key != key) {
        node = node.Next;
        if (node == sentinel) {
            return false; // Schlüssel nicht gefunden
        }
    }

    return true; // Schlüssel gefunden
}

```

