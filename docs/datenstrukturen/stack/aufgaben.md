# Stack

Implementieren Sie eine einfache Methode in C#, die die Elemente eines Stacks umkehrt.

```C#
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        Stack<int> originalStack = new Stack<int>();
        originalStack.Push(1);
        originalStack.Push(2);
        originalStack.Push(3);
        originalStack.Push(4);
        
        Console.WriteLine("Original Stack:");
        PrintStack(originalStack);

        Stack<int> reversedStack = ReverseStack(originalStack);

        Console.WriteLine("Reversed Stack:");
        PrintStack(reversedStack);
    }

    static Stack<T> ReverseStack<T>(Stack<T> stack)
    {
        Stack<T> reversedStack = new Stack<T>();
        
        while (stack.Count > 0)
        {
            reversedStack.Push(stack.Pop());
        }
        
        return reversedStack;
    }

    static void PrintStack<T>(Stack<T> stack)
    {
        foreach (var item in stack)
        {
            Console.WriteLine(item);
        }
    }
}
```

## Erklärung:

* Main-Methode: Hier wird ein Stack mit einigen Ganzzahlen erstellt und die Methode ReverseStack aufgerufen, um die Elemente umzukehren.
* ReverseStack-Methode: Diese Methode nimmt einen Stack als Parameter und erstellt einen neuen Stack. Sie verwendet eine Schleife, um alle Elemente des ursprünglichen Stacks zu entfernen und sie in den neuen Stack zu schieben, wodurch die Reihenfolge umgekehrt wird.
* PrintStack-Methode: Diese Hilfsmethode gibt die Elemente des Stacks auf der Konsole aus.
