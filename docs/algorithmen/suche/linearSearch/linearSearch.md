
# Linear Search

## Beschreibung
Lineare Suche ist ein Algorithmus, der auch unter dem Namen sequentielle Suche bekannt ist. Er ist der einfachste Suchalgorithmus überhaupt.

Die Aufgabe besteht darin, ein Element in einer Liste oder einem Array mit n Elementen zu finden. Man geht dazu die Liste Element für Element durch, bis man es gefunden hat. Der Suchaufwand wächst linear mit der Anzahl der Elemente in der Liste.

Die effizientere Binäre Suche kann nur bei geordneten Listen benutzt werden.

Für ungeordnete Listen existiert mit Lazy Select noch ein randomisierter Algorithmus, der mit relativ hoher Wahrscheinlichkeit das x-te Element einer Liste bezüglich einer Ordnung schneller als in linearer Zeit finden kann. 

## Komplexität

Die lineare Suche befindet sich in der Komplexitätsklasse O(n), da sie im schlechtesten Fall (wenn der gesuchte Wert nicht gefunden werden kann) n Vergleiche benötigt.

Wenn die Daten zufallsverteilt sind, dann werden im Schnitt (n+1)/2 Vergleichsoperationen benötigt.

Im besten Fall ist gleich das erste Element der Liste dasjenige, das man sucht.

Wenn die Anzahl der Elemente in einer Liste klein ist, dann ist es oft auch das effizienteste Verfahren. 

## Pseudocode

```
BEGINN LinearSearch

  EINGABE: (S)uchschlüssel, (A)rray

  VARIABLE: N = Anzahl Elemente im Array 'A'
  VARIABLE: SucheErfolgreich = falsch
  VARIABLE: i = 0

  FÜR i BIS N ODER SucheErfolgreich
    WENN A[i] = S
    DANN SucheErfolgreich = wahr

  WENN SucheErfolgreich = wahr
  DANN AUSGABE: i
  SONST AUSGABE: Suche nicht erfolgreich

ENDE
```

## Implementierung 
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
