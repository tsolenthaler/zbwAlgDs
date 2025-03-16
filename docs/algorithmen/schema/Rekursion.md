# Rekursion

## Fakultät
Hier ist ein einfaches Beispiel für die Implementierung der Fakultätsfunktion mit Rekursion in C#:

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.Write("Geben Sie eine Zahl ein, um die Fakultät zu berechnen: ");
        int n = int.Parse(Console.ReadLine());

        if (n < 0)
        {
            Console.WriteLine("Die Fakultät ist nur für nicht-negative ganze Zahlen definiert.");
        }
        else
        {
            long result = Fakultät(n);
            Console.WriteLine($"Die Fakultät von {n} ist {result}.");
        }
    }

    static long Fakultät(int n)
    {
        if (n == 0 || n == 1)
        {
            return 1; // Basisfälle: Fakultät(0) = 1, Fakultät(1) = 1
        }
        return n * Fakultät(n - 1); // Rekursive Berechnung
    }
}
```

### Erklärung:
1. **Main-Methode**: Hier wird der Benutzer aufgefordert, eine Zahl einzugeben, für die die Fakultät berechnet werden soll. Es wird überprüft, ob die eingegebene Zahl negativ ist, da die Fakultät nur für nicht-negative ganze Zahlen definiert ist. Wenn die Zahl gültig ist, wird die Fakultät berechnet und ausgegeben.

2. **Fakultät-Methode**: Diese Methode berechnet die Fakultät für eine gegebene Zahl `n`. Die Basisfälle sind definiert, sodass `Fakultät(0)` und `Fakultät(1)` beide 1 zurückgeben. Für alle anderen Werte wird die Methode rekursiv aufgerufen.

### Nutzung:
Um das Programm auszuführen, kopiere den Code in eine C#-Entwicklungsumgebung (z.B. Visual Studio) und führe das Programm aus. Gib eine nicht-negative ganze Zahl ein, und das Programm gibt die Fakultät dieser Zahl aus.

## Fibonacci

Hier ist ein einfaches Beispiel für die Implementierung der Fibonacci-Zahlenfolge mit Rekursion in C#:

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.Write("Geben Sie die Anzahl der Fibonacci-Zahlen ein: ");
        int n = int.Parse(Console.ReadLine());

        Console.WriteLine("Fibonacci-Zahlen:");
        for (int i = 0; i < n; i++)
        {
            Console.WriteLine(Fibonacci(i));
        }
    }

    static int Fibonacci(int n)
    {
        if (n <= 1)
        {
            return n; // Basisfälle: Fibonacci(0) = 0, Fibonacci(1) = 1
        }
        return Fibonacci(n - 1) + Fibonacci(n - 2); // Rekursive Berechnung
    }
}
```

### Erklärung:
1. **Main-Methode**: Hier wird der Benutzer aufgefordert, die Anzahl der Fibonacci-Zahlen einzugeben, die er sehen möchte. Dann wird eine Schleife verwendet, um die Fibonacci-Zahlen bis zur angegebenen Anzahl zu berechnen und auszugeben.

2. **Fibonacci-Methode**: Diese Methode berechnet die Fibonacci-Zahl für einen gegebenen Index `n`. Die Basisfälle sind definiert, sodass `Fibonacci(0)` 0 und `Fibonacci(1)` 1 zurückgibt. Für alle anderen Werte wird die Methode rekursiv aufgerufen.

### Nutzung:
Um das Programm auszuführen, kopiere den Code in eine C#-Entwicklungsumgebung (z.B. Visual Studio) und führe das Programm aus. Gib die Anzahl der Fibonacci-Zahlen ein, die du berechnen möchtest, und das Programm gibt die entsprechenden Werte aus.