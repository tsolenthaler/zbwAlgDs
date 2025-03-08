# Aufgaben

## 1. Aufgabe
In welcher Komplexitätsklasse befindet sich die Funktion f(n)

f(n) = 3n2 + 5n + 18

Komplexitätsklasse = O(n^2)

## 2. Aufgabe

In welcher Komplexitätsklasse befindet sich die Funktion f(n)?

f(n) = 100

Komplexitätsklasse = O(1)

## 3. Aufgabe

Berechnen Sie die Komplexität der Prozeduren (Aufgaben 3-6). Wie oft wird do_something() aufgerufen? Überprüfen Sie Ihre Lösungen, indem Sie die Prozeduren in C# implementieren und einen Zähler einbauen.

```C#
void Procedure1(int n) {
    for(int i=0; i<=n; i++) {       --> n + 1
        do_something(i,n);
    }
    for(int j=n; j>=0; j--) {       --> n + 1
        do_something(j,n);
    }
}
```
Komplexitätsklasse = 2n + 1 = O(n)

## 4. Aufgabe

```C#
void Procedure2(int n) {
    for(int i=0; i<n; i++) {            --> n
        for(int j=0; j<2*i; j++) {      --> 
            do_something(i,j,n);
        }
    }
}
```

In der Funktion `Procedure2` gibt es zwei verschachtelte Schleifen. Die äussere Schleife wird
von `i = 0` bis `i < n` ausgeführt, was bedeutet, dass sie insgesamt `n`-mal durchläuft. Die
innere Schleife ist von der aktuellen Iteration der äußeren Schleife abhängig und wird von
`j = 0` bis `j < 2*i` ausgeführt.
Um die gesamte Anzahl der Durchläufe zu ermitteln, müssen wir die Anzahl der Iterationen in
der inneren Schleife für jede Iteration der äusseren Schleife zusammenzählen. Dies lässt sich
wie folgt darstellen:
- Für `i = 0` läuft die innere Schleife `0` Mal.
- Für `i = 1` läuft die innere Schleife `2` Mal.
- Für `i = 2` läuft die innere Schleife `4` Mal.
- Für `i = 3` läuft die innere Schleife `6` Mal.
- Für `i = 4` läuft die innere Schleife `8` Mal.
- ...
- Für `i = n-1` läuft die innere Schleife `2*(n-1)` Mal.
Wir summieren also alle diese Ausführungen auf:
Gesamtanzahl der Durchläufe = (0 + 2 + 4 + 6 + 8 + ... + 2*(n-1)) *
    = 2*(0 + 1 + 2 + 3 + 4 + … + n-1)
    = 2*(𝑛(𝑛−1)/2)     ---> (Gausssche Summenformel **)
    = n(n-1)
    = O(n^2)

* In der ersten Schlaufe läuft i von 0 bis n-1 (weil i<n)
    * Gausssche Summenformel: 1 + 2 + 3 + 4 + ⋯ + 𝑛 = 𝑛(𝑛+1)/2 = 𝑛^2+/2
    In obiger Lösung wird jedoch nicht bis n sondern nur bis n-1 summiert. D.h. es wird ein n weniger summiert: 
    𝑛2+𝑛/2 − 𝑛 = 𝑛2+𝑛−2𝑛/2 = 𝑛2−𝑛/2 = 𝑛(𝑛−1)/2

## 5. Aufgabe

```C#
void Procedure3(int n) {
    for(int i=0; i<n; i++) {
        int j = 0;
        while(j < 2*n) {
            j++;
            do_something(i,j,n);
        }
    }
}
```

Für: i=0, i=1, i=2,… , i=n-1
    = 2*n + 2*n + 2*n + … + 2*n
    = 2*n*n
    = 2n^2
    = O(n^2)

oder als Erklärung:

Die for-Schleife läuft von `i = 0` bis `i < n`, also wird sie `n`-mal durchgeführt. Innerhalb der for-
Schleife gibt es eine while-Schleife, die mit `j` bei `0` beginnt und so lange läuft, bis `j < 2*n`
nicht mehr wahr ist. Für jede Iteration der for-Schleife wird die while-Schleife `2*n`-mal
durchlaufen, da `j` in jedem Durchgang um `1` erhöht wird, bis es den Wert `2*n` erreicht.

Da die äussere Schleife `n`-mal durchläuft und die innere Schleife für jede äussere Iteration
`2*n`-mal durchläuft, können wir die Gesamtanzahl der Durchläufe der inneren Schleife als
Produkt dieser beiden Zahlen berechnen:

Gesamtanzahl der Durchläufe = (n * 2 * n) = (2 * n^2) = O(n^2)

## 6. Aufgabe

```C#
void Procedure4(int n) {
    int j=n;
    while(j > 0) {
        j = j/2;
        do_something(i,j,n);
    }
}
```

Wie oft kann n durch 2 geteilt werden? → log2(n)
+1 da j>0 (statt j>1) → log2(n)+1
= O(log n)

oder 

Für: j=n, j=n/2, j=n/4, ..., j=2, j=1
1 + 1 + 1 + ... + 1 + 1 = log2(n)+1 = O(log n)