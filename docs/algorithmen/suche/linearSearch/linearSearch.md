
# Linear Search

Implementieren Sie eine Methode in C#, die eine lineare Suche in einem Array durchführt.

```C#
using System;

class Program
{
    static void Main()
    {
        int[] array = { 5, 3, 8, 4, 2 };
        int valueToFind = 4;

        int index = LinearSearch(array, valueToFind);

        if (index != -1)
        {
            Console.WriteLine($"Wert {valueToFind} gefunden an Index {index}.");
        }
        else
        {
            Console.WriteLine($"Wert {valueToFind} nicht gefunden.");
        }
    }

    static int LinearSearch(int[] array, int value)
    {
        for (int i = 0; i < array.Length; i++)
        {
            if (array[i] == value)
            {
                return i; // Wert gefunden, Index zurückgeben
            }
        }
        return -1; // Wert nicht gefunden
    }
}
```

## Erklärung:

* Die Methode LinearSearch nimmt ein Array und einen Wert als Parameter.
* Sie durchläuft das Array mit einer for-Schleife.
* Wenn der gesuchte Wert gefunden wird, gibt die Methode den Index des Wertes zurück.
* Wenn der Wert nicht gefunden wird, gibt die Methode -1 zurück.
