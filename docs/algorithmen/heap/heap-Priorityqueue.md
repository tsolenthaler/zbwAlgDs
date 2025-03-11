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


## Was ist der Unterschied zwischen einem BinarySearchTree und einem Heap Priorityqueue?

Ein Binary Search Tree (BST) und eine Heap Priority Queue sind beides Datenstrukturen, die zur Speicherung und Verwaltung von Daten verwendet werden, aber sie haben unterschiedliche Eigenschaften und Anwendungsfälle. Hier sind die Hauptunterschiede:

### Binary Search Tree (BST)

1. **Struktur**: Ein BST ist ein binärer Baum, bei dem jeder Knoten maximal zwei Kinder hat. Für jeden Knoten gilt, dass alle Werte im linken Teilbaum kleiner und alle Werte im rechten Teilbaum größer sind.

2. **Zugriffszeit**: Die durchschnittliche Zeitkomplexität für Such-, Einfüge- und Löschoperationen beträgt O(log n) in einem balancierten BST. Im schlimmsten Fall (z. B. bei einem nicht balancierten Baum) kann die Zeitkomplexität O(n) betragen.

3. **Sortierung**: Ein BST ermöglicht eine einfache In-Order-Traversierung, um die Elemente in aufsteigender Reihenfolge zu erhalten.

4. **Anwendungsfälle**: BSTs werden häufig verwendet, wenn eine dynamische Menge von Daten benötigt wird, bei der häufige Such-, Einfüge- und Löschoperationen erforderlich sind.

### Heap Priority Queue

1. **Struktur**: Ein Heap ist eine spezielle Baumstruktur, die entweder ein Min-Heap oder ein Max-Heap sein kann. In einem Min-Heap ist der Wert jedes Knotens kleiner oder gleich dem Wert seiner Kinder, während in einem Max-Heap der Wert jedes Knotens größer oder gleich dem Wert seiner Kinder ist. Heaps sind oft als vollständige Binärbäume implementiert.

2. **Zugriffszeit**: Die Zeitkomplexität für das Einfügen eines Elements und das Entfernen des Minimums (oder Maximums) beträgt O(log n). Der Zugriff auf das Minimum (oder Maximum) erfolgt in O(1).

3. **Sortierung**: Heaps sind nicht für die In-Order-Traversierung geeignet, da sie nicht die gleiche Sortierreihenfolge wie ein BST bieten. Sie sind jedoch nützlich für Sortieralgorithmen wie Heapsort.

4. **Anwendungsfälle**: Heaps werden häufig in Anwendungen verwendet, bei denen die Priorität von Elementen wichtig ist, wie z. B. in Warteschlangen, bei der Implementierung von Dijkstra's Algorithmus oder in anderen Algorithmen, die eine effiziente Zugriff auf das Minimum oder Maximum erfordern.

### Zusammenfassung

- **BST**: Gut für dynamische Mengen mit häufigen Such-, Einfüge- und Löschoperationen; ermöglicht einfache Sortierung.
- **Heap**: Gut für Prioritätswarteschlangen; ermöglicht schnellen Zugriff auf das Minimum oder Maximum, aber nicht auf die gesamte sortierte Reihenfolge.

Beide Datenstrukturen haben ihre eigenen Vor- und Nachteile, und die Wahl zwischen ihnen hängt von den spezifischen Anforderungen der Anwendung ab.

## was sind die grundlegenden Operationen eines Heaps
Ein Heap ist eine spezielle Baumstruktur, die bestimmte Eigenschaften aufweist, je nachdem, ob es sich um einen Min-Heap oder einen Max-Heap handelt. Die grundlegenden Operationen eines Heaps sind:

### 1. Einfügen (Insert)
- **Beschreibung**: Fügt ein neues Element in den Heap ein.
- **Vorgehen**: 
  - Das Element wird zunächst am Ende des Heaps (in der letzten Position des Arrays) hinzugefügt.
  - Danach wird das Element "nach oben" (up-heap oder bubble-up) verschoben, um die Heap-Eigenschaft wiederherzustellen. Dies geschieht, indem das Element mit seinem Elternknoten verglichen wird und gegebenenfalls vertauscht wird, bis die Heap-Eigenschaft erfüllt ist.
- **Zeitkomplexität**: O(log n)

### 2. Entfernen des Minimums/Maximums (Remove Min/Max)
- **Beschreibung**: Entfernt das kleinste Element (im Min-Heap) oder das größte Element (im Max-Heap) aus dem Heap.
- **Vorgehen**: 
  - Das Wurzelelement (das Minimum oder Maximum) wird entfernt.
  - Das letzte Element im Heap wird an die Wurzelposition verschoben.
  - Danach wird das Element "nach unten" (down-heap oder bubble-down) verschoben, um die Heap-Eigenschaft wiederherzustellen. Dies geschieht, indem das Element mit seinen Kindknoten verglichen wird und gegebenenfalls vertauscht wird, bis die Heap-Eigenschaft erfüllt ist.
- **Zeitkomplexität**: O(log n)

### 3. Zugriff auf das Minimum/Maximum (Peek)
- **Beschreibung**: Gibt das kleinste Element (im Min-Heap) oder das größte Element (im Max-Heap) zurück, ohne es zu entfernen.
- **Vorgehen**: Das Wurzelelement wird einfach zurückgegeben.
- **Zeitkomplexität**: O(1)

### 4. Erstellen eines Heaps (Heapify)
- **Beschreibung**: Wandelt ein unsortiertes Array in einen Heap um.
- **Vorgehen**: 
  - Dies kann durch die Anwendung der "down-heap"-Operation auf alle nicht-blattknoten des Baums erfolgen, beginnend von den letzten Elternknoten bis zur Wurzel.
- **Zeitkomplexität**: O(n)

### 5. Löschen des Heaps (Clear)
- **Beschreibung**: Entfernt alle Elemente aus dem Heap.
- **Vorgehen**: In der Regel wird einfach der Speicher, der für den Heap verwendet wird, freigegeben.
- **Zeitkomplexität**: O(1) (aber das Freigeben des Speichers kann je nach Implementierung variieren)

### Zusammenfassung
Die grundlegenden Operationen eines Heaps sind das Einfügen von Elementen, das Entfernen des Minimums oder Maximums, der Zugriff auf das Minimum oder Maximum und das Erstellen eines Heaps aus einem unsortierten Array. Diese Operationen ermöglichen es, Heaps effizient für verschiedene Anwendungen, wie z. B. Prioritätswarteschlangen, zu nutzen.

## was sind mögliche Anwendungen eines Heaps?

Heaps sind vielseitige Datenstrukturen, die in verschiedenen Anwendungen und Algorithmen eingesetzt werden. Hier sind einige der häufigsten Anwendungen von Heaps:

### 1. **Prioritätswarteschlangen**
- Heaps werden häufig zur Implementierung von Prioritätswarteschlangen verwendet, in denen Elemente mit unterschiedlichen Prioritäten verarbeitet werden. Der Zugriff auf das Element mit der höchsten oder niedrigsten Priorität erfolgt effizient.

### 2. **Heapsort**
- Heapsort ist ein effizienter Sortieralgorithmus, der einen Heap verwendet, um eine Liste von Elementen zu sortieren. Der Algorithmus hat eine Zeitkomplexität von O(n log n) und ist in der Lage, die Elemente in-place zu sortieren.

### 3. **Dijkstra's Algorithmus**
- In Graphenalgorithmen, wie Dijkstra's Algorithmus zur Berechnung der kürzesten Wege, wird ein Min-Heap verwendet, um die Knoten mit den geringsten Kosten effizient zu verwalten.

### 4. **Prim's Algorithmus**
- Ähnlich wie bei Dijkstra's Algorithmus wird ein Min-Heap auch in Prim's Algorithmus verwendet, um den minimalen Spannbaum eines Graphen zu finden.

### 5. **Kleinste oder größte k-Elemente**
- Heaps können verwendet werden, um die k kleinsten oder größten Elemente aus einer großen Menge von Daten effizient zu extrahieren. Ein Min-Heap kann verwendet werden, um die k kleinsten Elemente zu finden, während ein Max-Heap für die k größten Elemente verwendet werden kann.

### 6. **Medianfindung**
- Heaps können in Kombination verwendet werden, um den Median einer Datenmenge effizient zu finden. Ein Min-Heap und ein Max-Heap können verwendet werden, um die beiden Hälften der Daten zu verwalten, sodass der Median schnell abgerufen werden kann.

### 7. **Event-Simulation**
- In der Simulation von Ereignissen, wie z. B. in der Computeranimation oder der Netzwerk-Simulation, können Heaps verwendet werden, um Ereignisse nach ihrem Zeitpunkt zu priorisieren und zu verarbeiten.

### 8. **Job-Scheduling**
- In Betriebssystemen können Heaps verwendet werden, um Prozesse oder Jobs basierend auf ihrer Priorität zu planen und zu verwalten.

### 9. **Kombinierte Datenstrukturen**
- Heaps können auch in anderen Datenstrukturen wie Fibonacci-Heaps oder Binomial-Heaps verwendet werden, die zusätzliche Funktionen und Effizienz bieten.

### Zusammenfassung
Heaps sind eine leistungsfähige Datenstruktur, die in vielen Bereichen der Informatik und Softwareentwicklung Anwendung findet, insbesondere in Algorithmen, die mit Prioritäten, Sortierung und Graphen arbeiten. Ihre Effizienz bei bestimmten Operationen macht sie zu einer bevorzugten Wahl für viele Probleme.