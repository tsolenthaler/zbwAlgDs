---
tags:
  - MD02
  - Schema
  - Algorithmen
  - Fakultät
  - Fibonacci
---

# Algorithmen Schema

## Ziele

- [ ] Ich kennen die grundlegenden Algorithmen Schemas
- [ ] Ich kennen Beispiele für die verschiedenen Schemas
- [ ] Ich kann eigene Algorithmen unter Anwendung der verschiedenen Schemas implementieren

## Algorithmen Schema
* Verfahrensmuster bzw. allgemeine Methode für Problemlösung
* Nicht jede Methode ist für jedes Problem gleich gut geeignet
    * Deswegen ist es wichtig, die verschiedenen Schemas zu kennen

## Iteration
* Iteration - bspwl. Loop (while oder for-Schleife)
    * Algorithmus verwendet einen Loop (while- oder for-Schleife)
    * Beispiel: Daten in Array (oder List) und mit jedem Element müssen die gleichen Schritte durchgeführt werden
        * Lässt sich gut parallelisieren

```c#
public static BigInteger Factorial(int n) {
    BigInteger result = 1;
    for (var i = 1; i <= n; i++)
        result = result * i;
    return result;
}
```
## Rekursion
* Rekursion - bspw. Fibonacci
    * Fundamentales Konzept der Informatik
    * Ein Algorithmus heisst rekursiv, wenn er sich direkt oder indirekt selber aufruft
    * Wichtig: Abbruchbedingung, damit der Algorithmus in jedem Fall terminiert
    * Rekursion macht dort Sinn, wenn der Algorithmus dadurch klarer und kürzer wird
    * Rekursionselimination

### Beispiele

#### Beispiel 1
* Löse das Problem, indem du es auf das gleiche Problem, aber in kleinerem Masse zurückführst.
* Beispiel:
    * Fakultät
    * Problem
    * Wie berechne ich 4! ?
        * gleiches Problem, jedoch kleiner:
            * --> Wie berechne ich 3! ?
        * Wenn ich weiss, was 3! ist, so weiss ich auch was 4! ist
            * --> 4! = 1 * 2 * 3 * 4 = ( 1 * 2 * 3 ) * 4 = 3! * 4

* 2! = 1 * 2
* 3! = 1 * 2 * 3
* 4! = 1 * 2 * 3 * 4 = 3! * 4
* 5! = 1 * 2 * 3 * 4 * 5

#### Beispiel 2
* allgemein
    * n! = (n-1)! * n
    * Aufruf: n! = Problem "Grösse" n
    * Aufruf: (n-1)! = Problem "Grösse" n-1

#### Beispiel 3

n! = 1 = falls n=1 --> Terminierender Fall (n minimal)
n! = (n-1)! * n = falls n>1 --> Rekursiver Fall (n wird kleiner!)

#### Zusammengefasst
* Schreibweise in Pseudeocode
    * fac(n) = Fakultät = n!
* Lösung
    * Problem = fac(n)
    * Kleineres Problem = fac(n-1)
    * Wenn kleineres Problem gelöst = n * fac(n-1)
    * Trivialer Fall = fac(1) = 1
    * Unterscheidung kl. Problem / triv. Fall = n=1 --> Triv. Fall

#### Rekursion: Beispiel Code
```c#
public static BigInteger FactorialRecursive(int n) {
    if (n == 0)
        return 1;

    return n * FactorialRecursive(n - 1);
}
```

#### Rekursion – Beispiel Fibonacci
* Fibonacci-Reihe: 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …

fibonacci(1) = 1

fibonacci(2) = 1

fibonacci(n) = fibonacci(n-1)+fibonacci(n-2)

```c#
public static long FibonacciRecursive(long len) {
    if (len == 1 || len == 2) {
        return 1;
    }
    return FibonacciRecursive(len-1) + FibonacciRecursive(len-2);
}
```

Hinweis: FibonacciRecursive(6) berechnet die 6. Fibonacci-Zahl (=8)
* 1te Zahl = 1, 2te zahl = 1, 3te Zahl = 2, 4te Zahl = 3 usw.

#### Rekursion – Beispiel Fibonacci - Laufzeit
``` mermaid
flowchart TD
    1[F6]
    1 --> 2[F5]
    1 --> 3[F4]
    2 --> 4[F4]
    2 --> 5[F3]
    3 --> 6[F3]
    3 --> 7[F2]
    4 --> 8[F3]
    4 --> 9[F2]
    5 --> 10[F2]
    5 --> 11[F1]
    6 --> 12[F2]
    6 --> 21[F1]
    7 --> 13[1]
    8 --> 14[F2]
    8 --> 18[F1]
    9 --> 15[1]
    10 --> 16[1]
    11 --> 17[1]
    14 --> 19[1]
    18 --> 20[1]
    12 --> 22[1]
    21 --> 23[1]
```

### Rekursionselimination

* Prinzipielles Vorgehen
    * Umdrehen der Berechnung (von unten nach oben)
    * Abspeichern der Zwischenresultate

* Aufgabe: Implementieren Sie die Berechnung der Fibonacci-Zahl iterativ und vergleichen Sie anschliessend die Laufzeiten z.B. für Fibonacci(40)

!!! note "Hinweis"
    Mathe - Fibonacci
    Mathe - Fakultät

## Divide and Conquer
* Divide and Conquer - bspw. Türme von Hanoi
    * «Teile und Herrsche»
        * Ablauf:
            * Wenn das Problem trivial ist, dann löse es
            * Wenn das Problem nicht trivial ist, dann
                * Zerlege es in kleinere unabhängige Teilprobleme
                * Löse die (kleineren) Teilprobleme separat
                * Verbinde die Teillösungen zu einer Gesamtlösung

    * Bekannte Anwendungen für «Divide and Conquer» sind die Sortieralgorithmen «Quicksort» und «Mergesort»

    !!! tip "Anwendung"
    
        * «Quicksort»
        * «Mergesort»
    
    !!! example "Türme von Hanoi"

        * In einem Tempel im indischen Benares ruht eine Messingplatte in der drei Diamantnadeln befestigt sind.
        * Auf einer der Nadeln hat Gott 64 Scheiben aus Gold zu einem Turm aufgeschichtet, wobei jede Scheibe etwas kleiner ist, als die Scheibe auf der sie ruht.
        * Die Priester des Tempels sind Tag und Nacht damit beschäftigt, den Turm unter Beachtung folgender Regel auf eine der anderen Nadeln zu bewegen:
            * Die Scheiben sind so kostbar, dass sie nur auf den drei Diamantnadeln im Tempel aufgeschichtet werden dürfen.
            * Die Scheiben sind schwer und zerbrechlich, daher darf immer nur eine der Scheiben bewegt werden, niemals mehrere zur gleichen Zeit.
            * Niemals darf eine Scheibe auf einer kleineren Scheibe liegen.

## Greedy
* Greedy
    * Vor allem für Optimierungsprobleme
    * Arbeitet in Schritten, ohne mehr als einen Schritt voraus- oder zurückzublicken. Bei jedem Schritt wird aus einer Menge von möglichen Wegen derjenige ausgesucht, der den Bedingungen des Problems genügt und lokal optimal ist


## Zusammenfassung

* Gleiche Algorithmen können auf diverse Arten implementiert werden
* Nicht jede Art ist optimal
* Es gibt einen riesigen Fundus an bereits bestehenden Algorithmen. Wir werden einige aus verschiedenen Problemklassen anschauen.

--> Zentral ist die Fertigkeit, sein Problem abstrahieren zu können!

--> Lesen Sie Kapitel 1.4 in Cordts2014, Lösen Sie die Aufgaben zum Kapitel


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








