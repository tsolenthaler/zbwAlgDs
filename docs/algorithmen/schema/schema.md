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

* n! = 1 = falls n=1 --> Terminierender Fall (n minimal)
* n! = (n-1)! * n = falls n>1 --> Rekursiver Fall (n wird kleiner!)

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