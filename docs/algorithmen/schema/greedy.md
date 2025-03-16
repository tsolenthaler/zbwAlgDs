# Greedy

Hier ist ein einfaches Beispiel für die Implementierung eines Greedy-Algorithmus in C#. In diesem Beispiel verwenden wir den Greedy-Algorithmus, um das "Münzwechselproblem" zu lösen. Das Ziel ist es, einen bestimmten Betrag mit der minimalen Anzahl von Münzen zu erreichen.

Angenommen, wir haben Münzen mit den Werten 1, 5, 10 und 25 Cent, und wir möchten einen Betrag von 63 Cent erreichen.

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        int amount = 63; // Der Betrag, den wir erreichen wollen
        int[] coins = { 25, 10, 5, 1 }; // Die verfügbaren Münzwerte

        List<int> result = GetMinimumCoins(amount, coins);

        Console.WriteLine("Münzen für " + amount + " Cent:");
        foreach (int coin in result)
        {
            Console.WriteLine(coin + " Cent");
        }
    }

    static List<int> GetMinimumCoins(int amount, int[] coins)
    {
        List<int> result = new List<int>();

        // Sortiere die Münzen in absteigender Reihenfolge
        Array.Sort(coins);
        Array.Reverse(coins);

        foreach (int coin in coins)
        {
            while (amount >= coin)
            {
                amount -= coin; // Ziehe den Münzwert vom Betrag ab
                result.Add(coin); // Füge die Münze zur Ergebnisliste hinzu
            }
        }

        return result;
    }
}
```

### Erklärung des Codes:
1. **Main-Methode**: Hier definieren wir den Betrag, den wir erreichen möchten, und die verfügbaren Münzwerte. Wir rufen die Methode `GetMinimumCoins` auf, um die minimalen Münzen zu erhalten.

2. **GetMinimumCoins-Methode**: Diese Methode nimmt den Betrag und die Münzwerte als Parameter. Sie sortiert die Münzen in absteigender Reihenfolge und verwendet eine Schleife, um die größte Münze zu wählen, die den verbleibenden Betrag nicht überschreitet. Dies wird wiederholt, bis der Betrag auf 0 reduziert ist.

3. **Ergebnis**: Die Methode gibt eine Liste der verwendeten Münzen zurück, die dann in der Konsole ausgegeben wird.

### Ausführung:
Wenn Sie dieses Programm ausführen, wird es die Münzen ausgeben, die benötigt werden, um 63 Cent mit der minimalen Anzahl von Münzen zu erreichen. In diesem Fall könnte die Ausgabe wie folgt aussehen:
```
Münzen für 63 Cent:
25 Cent
25 Cent
10 Cent
1 Cent
1 Cent
```

Dieses Beispiel zeigt, wie der Greedy-Algorithmus funktioniert, indem er immer die größte verfügbare Münze auswählt, um den Betrag zu reduzieren.