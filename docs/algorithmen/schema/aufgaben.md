
## Aufgaben

### 1. Aufgabe
Analysieren Sie folgenden Algorithmus auf Korrektheit. Bringen Sie falls nötig Korrekturen an. 


```C#
public static int Factorial(int n) { 
    
        return n * Factorial(n - 1); 

}     
```

Antwort:

```C#
public static int Factorial(int n) { 
    if(n != 0) {
        return n * Factorial(n - 1); 
    } else {
        return 1;
    }
} 
```


### 2. Aufgabe
In welcher Komplexitätsklasse befindet sich die rekursive Variante des Fibonacci-Algorithmus? 
Wieso befindet sich die iterative Variante in einer anderen Komplexitätsklasse (welcher?)? 

* Komplexität ist höher bei der Rekursive Methode
* Rekursive =  O(2N) --> Alle Zwischenresultate werden immer wieder berechnet. (exponentielle)
* Iterative =  O(n) --> in einer Schleife nur ein mal berechnet.

### 3. Aufgabe 🔴
Um das Maximum einer Menge S mit n Elementen zu bestimmen, kann das folgende Divide-and-Conquer Verfahren angewendet werden: 
1. Divide: Zerlege die Menge S in zwei Teilmengen 𝑆1 und 𝑆2 mit |𝑆1|= (|𝑆|/2) und |𝑆2| = (|𝑆|/2) 
2. Conquer: Wende das Verfahren rekursiv an, um max(𝑆1) und max(𝑆2) zu berechnen. 
3. Combine: Berechne daraus max(𝑆). Überlegen Sie sich den trivialen Fall, der dann die Berechnung durchführt und die Rekursion abbricht. 

Formulieren Sie zu diesem Verfahren einen rekursiven Algorithmus in Pseudocode. 
 
Hinweise: 
* |𝑆1| = Anzahl Elemente der Menge 𝑆1 
* ⌊𝑥⌋  = x auf die nächst kleinere Ganzzahl abrunden (C#: Math.Floor()) 
* ⌈𝑥⌉  = x auf die nächst grössere Ganzzahl aufrunden (C#: Math.Ceiling())

#### Antwort (evlt. nicht korrekt)
Menge = {2,10,11,8,100,87,95,80,7}

s1 = S/2
s2 = S/2

max(s1) = s1.Math.Ceiling();  // grössere Ganzzahl abrunden

#### weiter Antworten:
```
Algorithm Max(S)
    Input: Eine Menge S mit n Elementen
    Output: Das Maximum der Menge S

    // Trivialer Fall: Wenn die Menge nur ein Element hat
    if |S| == 1 then
        return S[0] // Das einzige Element ist das Maximum

    // Divide: Zerlege die Menge in zwei Teilmengen
    mid = ⌊|S| / 2⌋
    S1 = S[0:mid] // Erste Hälfte
    S2 = S[mid:|S|] // Zweite Hälfte

    // Conquer: Berechne das Maximum der beiden Teilmengen
    max1 = Max(S1) // Maximum von S1
    max2 = Max(S2) // Maximum von S2

    // Combine: Berechne das Maximum aus den beiden Maxima
    return max(max1, max2) // Das Maximum von S
```

### 4. Aufgabe 🔴
Gegeben ist folgendes Programm: 

```C#
public class Recursion { 
    public static int Rec(int p1, int p2) { 
        if (p2 == 0) { 
            return 1; 
        } 
 
        if ((p2 % 2) != 0) { 
            int y = Rec(p1, (p2 - 1) / 2); 
            Console.WriteLine($"{p1} * {y} * {y}"); 
            return p1 * y * y; 
        } else { 
            int y = Rec(p1, p2 / 2); 
            Console.WriteLine($"{y} * {y}"); 
            return y * y; 
        } 
    } 

    public static void Main() { 
        Rec(2, 5); 
    } 
} 
```
 
Auf den beiden Zeilen 9 und 13 werden jeweils Multiplikationen durchgeführt. Zusätzlich werden die Multiplikationen auf der Konsole ausgegeben. 
In nachfolgender Tabelle sollen in zeitlicher Reihenfolge die Ausgaben des Programms (d.h. die Multiplikationen in zeitlicher Abfolge) notiert werden (z.B. «2 * 3 * 4»), für den Fall, dass Main() ausgeführt wird. 

1. Multiplikation: 2 * 1 * 1
2. Multiplikation: 2 * 2
3. Multiplikation: 2 * 4 * 4

#### Rekursion Schritt für Schritt:
* Erster Aufruf: Rec(2, 5)
    * p2 ist ungerade (5 % 2 != 0).
    * Aufruf: y = Rec(2, (5 - 1) / 2) = Rec(2, 2)

* Zweiter Aufruf: Rec(2, 2)
    * p2 ist gerade (2 % 2 == 0).
    * Aufruf: y = Rec(2, 2 / 2) = Rec(2, 1)

* Dritter Aufruf: Rec(2, 1)
    * p2 ist ungerade (1 % 2 != 0).
    * Aufruf: y = Rec(2, (1 - 1) / 2) = Rec(2, 0)

* Vierter Aufruf: Rec(2, 0)
    * p2 ist 0.
    * Rückgabe: 1

#### Rückkehr zu den vorherigen Aufrufen:
* Dritter Aufruf: Rec(2, 1)
    * y ist jetzt 1.
    * Ausgabe: 2 * 1 * 1 (Zeile 8)
    * Rückgabe: 2 * 1 * 1 = 2 (Zeile 9)

* Zweiter Aufruf: Rec(2, 2)
    * y ist jetzt 2.
    * Ausgabe: 2 * 2 (Zeile 12)
    * Rückgabe: 2 * 2 = 4 (Zeile 13)

* Erster Aufruf: Rec(2, 5)
    * y ist jetzt 4.
    * Ausgabe: 2 * 4 * 4 (Zeile 8)
    * Rückgabe: 2 * 4 * 4 = 32 (Zeile 9)


#### Start Main --> Rec(2,5)
1. Aufruf Zeile 7 - Rec(2, (5 - 1) / 2) = Rec(2, 2)
* 1.1. Rec(2, 2) = Rec(2, 1)
* 1.1.1. Rec(2, 1) = Rec(2, (1 - 1) / 2) = Rec(2,0)
* 1.1.1.1. Rec(2, 0) = return 1;
* 2.1.1. Rec(2,1)
Console.Write("2 * 1 * 1)
return 2 * 1 * 1
Rückgabe 2 * 1 * 1 = 2
* 2.1. Rec(2,2)
Console.Write("2 * 2)
Rückgabe 2 * 2 = 4
2. Rec(2,5)
Console.Write("2 * 4 * 4)
Rückgabe 2 * 4 * 4 = 32