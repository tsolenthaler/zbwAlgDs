# Komplexitätsklassen

| Komplexitätsklasse | Beschreibung | Beispiel |
| ------------------ | ------------ | -------- |
| `O(1)`             | Konstant: Die Komplexität ist unabhängig von der Anzahl der Eingabewerte n, d.h. die Anzahl beeinflusst nicht die Ausführungszeit. | ```public double GetPi() { return Math.Pi; }``` |
| `O(n)`             | Linear: Die Komplexität steigt linear mit der Anzahl der Eingabewerte. Beispiel: Alle Werte einmal durchlaufen. | ```public int GetCount(int[] array) { int n = 0; foreach (int i in array) n++; return n; }``` |
| `O(log(n))`        | Logarithmisch | ```void Procedure4(int n) { int j=n; while(j > 0) { j = j/2; do_something(i,j,n); } }``` |
| `O(n log(n))`      | Überlinear: Die Komplexität verhält sich loglinear zur Anzahl der Eingabewerte und liegt über der linearen Kurve. Beispiel: Sortalgorithmen wie MergeSort. |  |
| `O(n^2)`           | Quadratisch: Die Komplexität verhält sich quadratisch zur Anzahl der Eingabewerte. Beispiel: Sortierverfahren wie BubbleSort oder Vergleich jedes Wertes mit jedem anderen. | ```foreach (n1 in werte) { foreach(n2 in werte) { if(n1 == n2) ... } }``` |
| `O(n^k)`           | Polynomial: Die Komplexität verhält sich polynomial zur Anzahl der Eingabewerte. | ```foreach (n1 in werte) foreach(n2 in werte) foreach(n3 in werte) sum += n1 + n2 + n3;``` |


## Aufgabe 
### Aufgabenstellungen

1. **Konstante Komplexität (O(1))**
    - **Aufgabe:** 
    ```
    Implementiere eine Funktion, die immer denselben Wert zurückgibt, unabhängig von der Eingabe.
    ```
    - **Beispiel:** ```public double GetPi() { return Math.Pi; }```

2. **Lineare Komplexität (O(n))**
    - **Aufgabe:** 
    ```
    Implementiere eine Funktion, die die Anzahl der Elemente in einem Array zählt.
    ```
    - **Beispiel:** ```public int GetCount(int[] array) { int n = 0; foreach (int i in array) n++; return n; }```

3. **Logarithmische Komplexität (O(log(n)))**
    - **Aufgabe:** 
    ```
    Implementiere eine Funktion, die eine Schleife enthält, die die Eingabegröße bei jedem Schritt halbiert.
    ```
    - **Beispiel:** ```void Procedure4(int n) { int j=n; while(j > 0) { j = j/2; do_something(i,j,n); } }```

4. **Überlineare Komplexität (O(n log(n)))**
    - **Aufgabe:** 
    ```
    Implementiere einen Sortieralgorithmus wie MergeSort.
    ```
    - **Beispiel:** ```public void MergeSort(int[] array) { /* MergeSort Implementation */ }```

5. **Quadratische Komplexität (O(n^2))**
    - **Aufgabe:** 
    ```
    Implementiere eine Funktion, die jedes Element eines Arrays mit jedem anderen vergleicht.
    ```
    - **Beispiel:** ```foreach (n1 in werte) { foreach(n2 in werte) { if(n1 == n2) ... } }```

6. **Polynomiale Komplexität (O(n^k))**
    - **Aufgabe:** 
    ```
    Implementiere eine Funktion, die drei verschachtelte Schleifen enthält, die alle Kombinationen von Elementen eines Arrays durchlaufen.
    ```
    - **Beispiel:** ```foreach (n1 in werte) foreach(n2 in werte) foreach(n3 in werte) sum += n1 + n2 + n3;```