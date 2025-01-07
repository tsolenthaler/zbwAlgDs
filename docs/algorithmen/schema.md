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


* Divide and Conquer - bspw. Türme von Hanoi
* Greedy


## Zusammenfassung

* Gleiche Algorithmen können auf diverse Arten implementiert werden
* Nicht jede Art ist optimal
* Es gibt einen riesigen Fundus an bereits bestehenden Algorithmen. Wir werden einige aus verschiedenen Problemklassen anschauen.

--> • Zentral ist die Fertigkeit, sein Problem abstrahieren zu können!

--> Lesen Sie Kapitel 1.4 in [Cordts2014], Lösen Sie die Aufgaben zum Kapitel