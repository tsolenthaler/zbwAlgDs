---
tags:
  - MD02
  - Schema
  - Algorithmen
  - Fakultät
  - Fibonacci
---

# Algorithmen Schema

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

```c#
public static BigInteger FactorialRecursive(int n) {
    if (n == 0)
        return 1;

    return n * FactorialRecursive(n - 1);
}
```
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

--> Lesen Sie Kapitel 1.4 in [Cordts2014], Lösen Sie die Aufgaben zum Kapitel