# Iteration Fakultät

Hier ist ein einfaches Beispiel für die Berechnung der Fakultät einer Zahl mithilfe einer iterativen Methode in C#:

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.Write("Geben Sie eine positive ganze Zahl ein: ");
        int zahl = Convert.ToInt32(Console.ReadLine());

        if (zahl < 0)
        {
            Console.WriteLine("Die Fakultät ist nur für nicht-negative ganze Zahlen definiert.");
        }
        else
        {
            long fakultät = BerechneFakultät(zahl);
            Console.WriteLine($"Die Fakultät von {zahl} ist {fakultät}.");
        }
    }

    static long BerechneFakultät(int n)
    {
        long ergebnis = 1;

        for (int i = 1; i <= n; i++)
        {
            ergebnis *= i;
        }

        return ergebnis;
    }
}
```

### Erklärung des Codes:

1. **Main-Methode**: Hier wird der Benutzer aufgefordert, eine positive ganze Zahl einzugeben. Die Eingabe wird in eine Ganzzahl umgewandelt.

2. **Eingabevalidierung**: Es wird überprüft, ob die eingegebene Zahl negativ ist. Wenn ja, wird eine entsprechende Nachricht ausgegeben.

3. **BerechneFakultät-Methode**: Diese Methode berechnet die Fakultät der gegebenen Zahl `n` iterativ. Sie initialisiert eine Variable `ergebnis` mit 1 und multipliziert sie in einer Schleife mit jeder Zahl von 1 bis `n`.

4. **Ausgabe**: Schließlich wird das Ergebnis der Fakultätsberechnung ausgegeben.

### Verwendung:
Kopiere den Code in eine C#-Entwicklungsumgebung (z.B. Visual Studio) und führe das Programm aus. Gib eine positive ganze Zahl ein, um die Fakultät zu berechnen.