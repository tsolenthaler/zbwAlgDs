# Linear Search mit Sentinel

Der Linear Search mit Sentinel ist eine Technik zur Suche in einer Liste oder einem Array, die die Effizienz der Suche verbessert, indem ein Sentinel-Wert (ein spezieller Wert) am Ende der Liste hinzugefügt wird. Dies ermöglicht es, die Schleife zu vereinfachen, da man nicht ständig die Grenzen der Liste überprüfen muss. Hier ist eine detaillierte Erklärung, wie der Linear Search mit Sentinel in C# funktioniert:

### Grundprinzip des Linear Search

Der Linear Search (lineare Suche) durchsucht ein Array oder eine Liste, indem er jedes Element nacheinander überprüft, bis das gesuchte Element gefunden wird oder das Ende der Liste erreicht ist. Der Algorithmus hat eine Zeitkomplexität von O(n), da im schlimmsten Fall jedes Element überprüft werden muss.

### Sentinel-Linear-Suche

Die Sentinel-Technik verbessert die Effizienz, indem sie einen Sentinel-Wert am Ende des Arrays hinzufügt. Dieser Sentinel-Wert ist in der Regel der Wert, den wir suchen, oder ein Wert, der größer ist als alle anderen Werte im Array. Dadurch kann die Schleife vereinfacht werden, da wir nicht mehr überprüfen müssen, ob wir das Ende des Arrays erreicht haben.

### Implementierung in C#

Hier ist ein Beispiel, wie man eine lineare Suche mit Sentinel in C# implementieren kann:

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] array = { 3, 5, 2, 8, 6, 1 };
        int target = 8;

        int index = LinearSearchWithSentinel(array, target);

        if (index != -1)
        {
            Console.WriteLine($"Element {target} gefunden an Index: {index}");
        }
        else
        {
            Console.WriteLine($"Element {target} nicht gefunden.");
        }
    }

    static int LinearSearchWithSentinel(int[] array, int target)
    {
        int n = array.Length;

        // Sentinel-Wert hinzufügen
        int lastElement = array[n - 1];
        array[n - 1] = target;

        int i = 0;

        // Suche nach dem Zielwert
        while (array[i] != target)
        {
            i++;
        }

        // Wiederherstellen des letzten Elements
        array[n - 1] = lastElement;

        // Überprüfen, ob das gefundene Element das gesuchte ist
        if (i < n - 1 || array[n - 1] == target)
        {
            return i; // Index des gefundenen Elements
        }
        else
        {
            return -1; // Element nicht gefunden
        }
    }
}
```

### Erklärung des Codes

1. **Hinzufügen des Sentinel-Werts**: Der letzte Wert des Arrays wird gespeichert, und der Sentinel-Wert (in diesem Fall der gesuchte Wert) wird an die letzte Position des Arrays gesetzt.

2. **Durchführen der Suche**: Eine Schleife wird verwendet, um durch das Array zu iterieren, bis der Sentinel-Wert gefunden wird. Da der Sentinel-Wert am Ende des Arrays steht, wird die Schleife immer mindestens einmal durchlaufen.

3. **Wiederherstellen des letzten Elements**: Nach der Suche wird der ursprüngliche letzte Wert des Arrays wiederhergestellt.

4. **Überprüfen des Ergebnisses**: Am Ende wird überprüft, ob der gefundene Index innerhalb der Grenzen des Arrays liegt und ob das gefundene Element tatsächlich das gesuchte Element ist. Wenn ja, wird der Index zurückgegeben; andernfalls wird -1 zurückgegeben, um anzuzeigen, dass das Element nicht gefunden wurde.

### Fazit

Die Verwendung eines Sentinel-Werts in der linearen Suche kann die Effizienz des Algorithmus verbessern, indem die Notwendigkeit entfällt, die Grenzen des Arrays in jeder Iteration zu überprüfen. Dies kann insbesondere bei großen Arrays von Vorteil sein.