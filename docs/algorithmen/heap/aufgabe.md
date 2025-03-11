# Aufgaben Heap

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