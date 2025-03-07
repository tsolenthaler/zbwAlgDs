# Rucksackproblem

Das Rucksackproblem (Knapsack Problem) ist ein klassisches Problem der kombinatorischen Optimierung. Es gibt verschiedene Ansätze zur Lösung, darunter die dynamische Programmierung und die rekursive Methode. Hier ist eine einfache Implementierung des Rucksackproblems in C# unter Verwendung der dynamischen Programmierung:

```C#
using System;

class Program
{
    // Funktion zur Lösung des Rucksackproblems
    static int Knapsack(int capacity, int[] weights, int[] values, int n)
    {
        // Erstellen einer Tabelle zur Speicherung der maximalen Werte
        int[,] dp = new int[n + 1, capacity + 1];

        // Füllen der Tabelle
        for (int i = 0; i <= n; i++)
        {
            for (int w = 0; w <= capacity; w++)
            {
                if (i == 0 || w == 0)
                {
                    dp[i, w] = 0; // Basisfall
                }
                else if (weights[i - 1] <= w)
                {
                    // Maximalwert, wenn das aktuelle Element einbezogen wird oder nicht
                    dp[i, w] = Math.Max(values[i - 1] + dp[i - 1, w - weights[i - 1]], dp[i - 1, w]);
                }
                else
                {
                    dp[i, w] = dp[i - 1, w]; // Element kann nicht einbezogen werden
                }
            }
        }

        return dp[n, capacity]; // Der maximale Wert für die gegebene Kapazität
    }

    static void Main(string[] args)
    {
        int capacity = 50; // Kapazität des Rucksacks
        int[] weights = { 10, 20, 30 }; // Gewichte der Gegenstände
        int[] values = { 60, 100, 120 }; // Werte der Gegenstände
        int n = values.Length; // Anzahl der Gegenstände

        int maxValue = Knapsack(capacity, weights, values, n);
        Console.WriteLine("Der maximale Wert, der in den Rucksack passt, ist: " + maxValue);
    }
}
```

## Erklärung:

* Knapsack-Methode: Diese Methode verwendet eine 2D-Tabelle (dp), um die maximalen Werte für verschiedene Kapazitäten und Gegenstände zu speichern.
* Schleifen: Die äußere Schleife iteriert über die Anzahl der Gegenstände, während die innere Schleife über die möglichen Kapazitäten des Rucksacks iteriert.
* Bedingungen: Wenn das Gewicht des aktuellen Gegenstands kleiner oder gleich der aktuellen Kapazität ist, wird der maximale Wert berechnet, indem entweder der Gegenstand einbezogen oder ausgeschlossen wird.
* Hauptmethode: Hier werden die Kapazität, Gewichte und Werte der Gegenstände definiert und die Knapsack-Methode aufgerufen, um den maximalen Wert zu berechnen.
