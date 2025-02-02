# Lineare Datenstrukturen

## Aufgaben

### 1. Aufgabe
Die Nodes einer LinkedList werden in einem zusammenhängenden Speicherbereich gespeichert. Richtig  oder Falsch? Begründen Sie. 

* Falsch. Note verweist auf den Speicher

### 2. Aufgabe
Wenn temp den letzten Node in einer Doubly Linked List referenziert, welche Anweisung löscht diesen aus der Linked List? 
 
1) temp.Prev = null 
2) temp.Next.Prev = null 
3) temp.Prev.Next = null 

* 3. Ist korrekt. Prev geht eins Zurück und Löscht den Next

### 3. Aufgabe
Welche Komplexitätsklasse weisst LinkedList.Add(o) auf? Welche LinkedList.Remove(o)? Begründen Sie.

* LinkedList.Add() = O(1)
    * 
* LinkedList.Remove() = O(n) - linear
    * Zuerst finden/suchen des Knoten und jeden Knoten überprüft werden muss

### 4. Aufgabe
Wieso weisst der Zugriff auf ein Element in einem Array (array[i]) die Komplexitätsklasse O(1) auf, der Zugriff in einer LinkedList (linkedList[i]) jedoch O(n)? 

* Weile alle Element mit einer For Schlaufe durchsucht werden müssen bei einer LinkedList.
* Nicht zusammenhängende Knoten.

### 5. Aufgabe
Gegeben Sie den Inhalt des Stack S am Ende der folgenden Operationen an:

```C#
S.Push(3); 

S.Push(7); 

S.Pop(); 

S.Push(9); 

S.Peek(); 

S.Push(7); 

S.Push(1); 

S.Push(81); 

S.Pop(); 

S.Pop();
```

Der Stack soll nach jeder Operation dargestellt werden.

1. S: 3
2. S: 3, 7
3. S: 3
4. S: 3, 9
5. S: 3, 9
6. S: 3, 9, 7
7. S: 3, 9, 7, 1
8. S: 3, 9, 7, 1, 81
9. S: 3, 9, 7, 1
10. S: 3, 9, 7

Der endgültige Inhalt des Stacks S ist also: 3, 9, 7
