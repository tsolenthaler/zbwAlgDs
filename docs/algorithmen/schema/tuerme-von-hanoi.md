# Türme von Hanoi

Hier ist ein einfaches Beispiel für die Implementierung des Türme von Hanoi in C#. Dieses Programm verwendet eine rekursive Methode, um die Platten von einem Turm auf einen anderen zu bewegen.

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        int n = 3; // Anzahl der Platten
        Console.WriteLine("Die Schritte zur Lösung des Türme von Hanoi mit " + n + " Platten:");
        TowerOfHanoi(n, 'A', 'C', 'B'); // A, C und B sind die Namen der Türme
    }

    static void TowerOfHanoi(int n, char source, char destination, char auxiliary)
    {
        if (n == 1)
        {
            Console.WriteLine($"Bewege Platte 1 von Turm {source} nach Turm {destination}");
            return;
        }
        
        // Bewege n-1 Platten von source nach auxiliary, unter Verwendung von destination als Hilfsturm
        TowerOfHanoi(n - 1, source, auxiliary, destination);
        
        // Bewege die letzte Platte von source nach destination
        Console.WriteLine($"Bewege Platte {n} von Turm {source} nach Turm {destination}");
        
        // Bewege die n-1 Platten von auxiliary nach destination, unter Verwendung von source als Hilfsturm
        TowerOfHanoi(n - 1, auxiliary, destination, source);
    }
}
```

### Erklärung des Codes:
1. **Main-Methode**: Hier wird die Anzahl der Platten (`n`) festgelegt und die Methode `TowerOfHanoi` aufgerufen.
2. **TowerOfHanoi-Methode**: Diese Methode implementiert die Logik des Problems:
   - Wenn nur eine Platte vorhanden ist, wird sie direkt vom Quellturm zum Zielturm bewegt.
   - Andernfalls wird zuerst die oberste `n-1` Platte auf den Hilfsturm bewegt, dann die `n`-te Platte auf den Zielturm, und schließlich die `n-1` Platten vom Hilfsturm auf den Zielturm bewegt.

### Ausführung:
Wenn du das Programm ausführst, wird es die Schritte ausgeben, die erforderlich sind, um die Platten von einem Turm auf einen anderen zu bewegen. Du kannst die Anzahl der Platten (`n`) ändern, um zu sehen, wie sich die Anzahl der Schritte ändert.