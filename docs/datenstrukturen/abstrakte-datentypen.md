---
tags:
  - MD02
  - Abstrakte Datentypen
  - Datensturkturen
---

# Abstrakte Datentypen - Datensturkturen

## Definiton (ADT)

Datentypen sind in einer Programmiersprache vorhandenen 

* Grundtypen, wie int, boolean, real, char, ... und
* Strukturiertungsmethoden, wie array, struct, ...

und die darauf defineriten Operationen wie 
+ (Addition, Stringkonkatenation), *, sqrt, [] (Selektion),...

### Anmerkung:

* Datentypen hängen von der Programmiersprache ab.
* Es gibt heute ein Verständnis über "übliche" Datentypen:
    * ganz Zahlen, Fliesskommazahlen, Zeichen, Zeichenketten.
    * Gruppierung gleichartiger und verschiedener Datentypen.


### ADT (abstrakter Datentyp)
* Ein Datentyp, d.h.
    * eine **Menge** von ***Werten** und
    * **Operationen** auf diesen Werten,
    * der **nur** über eine Schnittstelle zugänglich ist, sowie
    * **Regeln** über die Wirkung der Operationen auf den Werten.

### Implementierung (eines ADT)
* Ein Programm, das den Datentyp realisiert.

Anmerkung
* Zur Implementierung eines ADT werden typischerweise Datenstrukturen aus
vorhandenen Datentypen gebildet, z.B. int A [] = new int[10]; int length = 0;

## Beispiele
### List Abstract Data Type
Contains elements of same type arranged in sequential order

* Initialize() - Initialize the list to be empty.
* get() - Return an element from the list at any given position.
* insert() - Insert a new element at any position of the list.
* remove() - Remove first occurrence of any element from a non empty list.
* removeAt() - Remove the element at a specified location from a non empty list.
* replace() - Replace an element at any position by another element.
* size() - Return the number of elements in the list.
* isEmpty() - Return true if the list is empty, otherwise return false.
* isFull() - Return true if the list is full, otherwise return false.

### Stack Abstract Data Type
Contains elements of same type arranged in sequential order

* Initailize() - Initialize the stack to be empty.
* Push() - Insert an element at one end of the stack called top.
* Pop() - Remove and return the element at the top of the stack
* Peek() - Return the element at the top of the stack without removing it
* size() - Return the number of elements in the stack.
* isEmpty() - Return true if stack is empty
* isFull() - Return true if no more elements can be pushed

## Anmerkung
C# unterstutzt den Umgang mit ADT's durch die Bereitstellung von Klassenund Interfaces.

List und Stack kann nun konkret als Array oder als verkettete Liste implementiert werden.

Die verwendete Implementierung hängt von der konkreten Anwendung ab:
* Datenvolumen
* Geschwindigkeit

## Abstrakte Datentypen vs. Datenstrukturen

Datenstruktur ist die physikalische Implementierung eines abstrakten Datentyp.

### Abstrakter Datentyp
Logische Sicht auf die Daten und den Operationen um die Daten zu manipulieren

### Datenstruktur
Konkrete Repräsentation der Daten und Algorithmen um die Daten zu manipulieren
