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