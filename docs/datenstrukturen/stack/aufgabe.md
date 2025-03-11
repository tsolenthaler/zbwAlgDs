## Aufgaben Stack 🔴

### 1.Aufgabe - Generischer Stack
Implementieren Sie einen generischen Stack<T> mit den Operationen Push(x) und x = Pop(). Pop soll dasjenige Element liefern, das zuletzt mit Push gespeichert wurde. Implementieren Sie auch ein Property Size, das die Anzahl der Elemente im Stack liefert. Schreiben Sie ein Testprogramm, das Kommandozeilenargumente in einem Stack<string> und die Längen der Kommandozeilenargumente in einem Stack<int> ablegt

```C#
using System;
using System.Collections.Generic;

public class Stack<T>
{
    private List<T> elements = new List<T>();

    public void Push(T item)
    {
        elements.Add(item);
    }

    public T Pop()
    {
        if (elements.Count == 0)
        {
            throw new InvalidOperationException("Der Stack ist leer.");
        }
        T item = elements[elements.Count - 1];
        elements.RemoveAt(elements.Count - 1);
        return item;
    }

    public int Size
    {
        get { return elements.Count; }
    }
}
```

#### Testprogramm
```C#
class Program
{
    static void Main(string[] args)
    {
        Stack<string> stringStack = new Stack<string>();
        Stack<int> intStack = new Stack<int>();

        foreach (string arg in args)
        {
            stringStack.Push(arg);
            intStack.Push(arg.Length);
        }

        Console.WriteLine("Kommandozeilenargumente und ihre Längen:");
        while (stringStack.Size > 0)
        {
            string str = stringStack.Pop();
            int length = intStack.Pop();
            Console.WriteLine($"Argument: {str}, Länge: {length}");
        }
    }
}
```

### 2.Aufgabe - Vererbung
Implementieren Sie eine generische Klasse StackExtended<T> als Unterklasse der in Aufgabe 1 implementierten Klasse Stack<T>. Darin soll es eine Methode Contains(x) geben, die prüft, ob das Element x im Stack vorhanden ist oder nicht. Ferner soll es einen Indexer geben, mit dem man auf die einzelnen Stack-Elemente zugreifen kann.

```C#
using System;

public class Stack<T>
{
    private T[] elements;
    private int top;

    public Stack(int size)
    {
        elements = new T[size];
        top = -1;
    }

    public void Push(T item)
    {
        if (top == elements.Length - 1)
            throw new InvalidOperationException("Stack overflow");
        elements[++top] = item;
    }

    public T Pop()
    {
        if (IsEmpty())
            throw new InvalidOperationException("Stack underflow");
        return elements[top--];
    }

    public bool IsEmpty()
    {
        return top == -1;
    }

    public int Count
    {
        get { return top + 1; }
    }
}

public class StackExtended<T> : Stack<T>
{
    public StackExtended(int size) : base(size) { }

    public bool Contains(T item)
    {
        for (int i = 0; i <= Count - 1; i++)
        {
            if (elements[i].Equals(item))
            {
                return true;
            }
        }
        return false;
    }

    public T this[int index]
    {
        get
        {
            if (index < 0 || index >= Count)
                throw new IndexOutOfRangeException("Index out of range");
            return elements[index];
        }
    }
}
```

### 3. Aufgabe - Fibonacci
Verwenden Sie einen Stack, um die Fibonacci-Folge iterativ bis zu einer gewünschten Zahl zu berechnen. Die gewünschte Zahl soll von der Console eingelesen werden. Für die Berechnung dürfen Sie ausschliesslich einen Stack<long> (gemäss Aufgabe 1) und eine for-Schlaufe verwenden. Am Schluss soll das Resultat auf der Console ausgegeben werden.

Beispiele:

* Eingabe = 7 → Ausgabe = 13
* Eingabe = 15 → Ausgabe = 610
* Eingabe = 33 → Ausgabe = 3524578

```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        Console.Write("Geben Sie die gewünschte Zahl ein: ");
        int n = int.Parse(Console.ReadLine());

        if (n < 0)
        {
            Console.WriteLine("Bitte geben Sie eine nicht-negative Zahl ein.");
            return;
        }

        // Stack für die Fibonacci-Zahlen
        Stack<long> stack = new Stack<long>();

        // Initiale Werte für die Fibonacci-Folge
        long a = 0; // F(0)
        long b = 1; // F(1)

        // Wenn n 0 ist, geben wir 0 zurück
        if (n == 0)
        {
            Console.WriteLine(a);
            return;
        }

        // Wenn n 1 ist, geben wir 1 zurück
        if (n == 1)
        {
            Console.WriteLine(b);
            return;
        }

        // Berechnung der Fibonacci-Zahl bis n
        for (int i = 2; i <= n; i++)
        {
            long next = a + b; // F(n) = F(n-1) + F(n-2)
            stack.Push(next);   // Speichern der aktuellen Fibonacci-Zahl im Stack
            a = b;              // Verschieben der Werte
            b = next;
        }

        // Das Ergebnis ist die oberste Zahl im Stack
        long result = stack.Pop();
        Console.WriteLine(result);
    }
}
```
