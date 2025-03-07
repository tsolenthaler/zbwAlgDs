---
tags:
  - Stack
hide:
  #- navigation
  #- toc
---

# Stack

## Definition Stack

* Deutsch: Stapel, Keller, LIFO-Speicher (Last-in-First-out)
* Ablegen und Entnahme der Elemente von oben, d.h. die Elemente, die zuletzt eingefügt wurden, werden als nächstes wieder entnommen (Last-in-First-out).

## Beispiel

* Türme von Hanoi
* Tellerstabel
* 

## Funktionsweise

Zeichnung mit mermaid

### Ablauf 1

* Einfügen: Push
* Löschen: Pop

Push P

![alt text](stack1.png)

### Ablauf 2

Push Q

![alt text](stack2.png)

### Ablauf 3

Push S

![alt text](stack3.png)

### Ablauf 4

Pop

Popped Item = S

![alt text](stack4.png)

### Ablauf 5

Pop

Popped Item = S

Popped Item = Q

![alt text](stack5.png)

## Implementierung

* Welche Methoden und Eigenschaften sollen für einen Stack implementiert werden?

```C#
public void Push(T item)
public T Pop()
public T Peek()
public void Clear()
public int Count
```

```C#
public class Stack<T>
{
    private List<T> elements = new List<T>();

    public void Push(T item)
    {
        elements.Add(item);
    }

    public T Pop()
    {
        if (elements.Count == 0) throw new InvalidOperationException("Stack is empty.");
        T item = elements[elements.Count - 1];
        elements.RemoveAt(elements.Count - 1);
        return item;
    }

    public T Peek()
    {
        if (elements.Count == 0) throw new InvalidOperationException("Stack is empty.");
        return elements[elements.Count - 1];
    }

    public void Clear()
    {
        elements.Clear();
    }

    public int Count
    {
        get { return elements.Count; }
    }
}
```


* Implementierung als
    * Array
    * SinglyLinkedList

### Implementierung als Array

![Implementierung als Array](stackArray.png)

### Implementierung als SinglyLinkedList

![alt text](stackSinglyLinkedList.png)

## Spezialfälle

* Beim Stack müssen üblicherweise zwei Spezialfälle näher betrachtet werden:
    * Overflow:
        * Der Stack überläuft – d.h. das Array hat keinen Platz mehr. Entweder wird das Array vergrössert oder der 	Aufrufer erhält eine Fehlermeldung und die Operation Push() wird abgebrochen
    * Underflow:
        * Es wird auf einen leeren Stack die Operation Pop() ausgeführt. Der Aufrufer erhält eine Fehlermeldung und die Operation Pop() wird abgebrochen.

## Selbststudium

* Lesen Sie Kapitel 2.3 in Cordts2023, Lösen Sie die Aufgaben zum Kapitel
* Bearbeiten Sie die Beispiele in Cordts2023 (Beachten Sie auch die Quellcodes zum Buch – siehe Slides «Einführung»):
    * PostScript (S. 58ff)
    * FloodFill-Algorithmus (S. 62ff)


## Aufgaben 🔴

### 1.Aufgabe - Generischer Stack
Implementieren Sie einen generischen Stack<T> mit den Operationen Push(x) und x = Pop(). Pop soll dasjenige Element liefern, das zuletzt mit Push gespeichert wurde. Implementieren Sie auch ein Property Size, das die Anzahl der Elemente im Stack liefert. Schreiben Sie ein Testprogramm, das Kommandozeilenargumente in einem Stack<string> und die Längen der Kommandozeilenargumente in einem Stack<int> ablegt

### 2.Aufgabe - Vererbung
Implementieren Sie eine generische Klasse StackExtended<T> als Unterklasse der in Aufgabe 1 implementierten Klasse Stack<T>. Darin soll es eine Methode Contains(x) geben, die prüft, ob das Element x im Stack vorhanden ist oder nicht. Ferner soll es einen Indexer geben, mit dem man auf die einzelnen Stack-Elemente zugreifen kann.

### 3. Aufgabe - Fibonacci
Verwenden Sie einen Stack, um die Fibonacci-Folge iterativ bis zu einer gewünschten Zahl zu berechnen. Die gewünschte Zahl soll von der Console eingelesen werden. Für die Berechnung dürfen Sie ausschliesslich einen Stack<long> (gemäss Aufgabe 1) und eine for-Schlaufe verwenden. Am Schluss soll das Resultat auf der Console ausgegeben werden.

Beispiele:

* Eingabe = 7 → Ausgabe = 13
* Eingabe = 15 → Ausgabe = 610
* Eingabe = 33 → Ausgabe = 3524578
