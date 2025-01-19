---
tags:
  - komplexitätsklassen
  - o-notation
hide:
  - navigation
  - toc
---

# Komplexitätsklassen

### Übungen 

- **Promt:** 
    ```
    Erstelle mir eine Aufgabe welche zufällig eine von diesen Komplexitätsklasse von O(1), O(n), O(log(n)), O(n log(n)), O(n^2) oder O(n^k) verwendet und ich die Komplexität bei einem C# Beispiel berechnen muss.
    ```

## Komplexitätsklassen

![Komplexitätsklassen](https://images.squarespace-cdn.com/content/v1/5c5c91c1b7c92c593c4f65b1/1634157762557-YMNNZPL0011WZW1M2NW3/big-o-notation-graph.png){ align=left }

| #       | Komplexitätsklasse | Beschreibung | Beispiel |
| ------- | ------------------ | ------------ | -------- |
|  | `O(1)`             |  **Konstant** - Ein Algorithmus, der unabhängig von der Größe des Datensatzes immer in der gleichen Zeit ausführt, unabhängig von der Größe des Datensatzes. Effizient bei jedem Datensatz. | ```public double GetPi() { return Math.Pi; }``` |
| | `O(log(n))`        | **Logarithmisch** - Ein Algorithmus, der den Datensatz in jedem Durchgang halbiert. Im Gegensatz zu exponentiell. Effizient bei großen Datensätzen. | ```void Procedure4(int n) { int j=n; while(j > 0) { j = j/2; do_something(i,j,n); } }``` |
|  | `O(n)`             | **Linear** - Ein Algorithmus, dessen Leistung mit wachsendem Datensatz abnimmt wächst. Reduziert die Effizienz bei immer größeren Datensätzen. | ```public int GetCount(int[] array) { int n = 0; foreach (int i in array) n++; return n; }``` |
|  | `O(n log(n))`      | **Überlinear** - Die Komplexität verhält sich loglinear zur Anzahl der Eingabewerte und liegt über der linearen Kurve. <br/>Beispiel: Sortalgorithmen wie MergeSort: <br/>- bei linearer Laufzeit verdoppelt sich die Laufzeit bei Verdoppelung der Eingabewerte <br/>- bei konstanter Laufzeit bleibt die Laufzeit bei Verdoppelung der Eingabewerte gleich <br/>- bei quadratischer Laufzeit steigt die Laufzeit bei Verdoppelung der Eingabewerte quadratisch an|  |
|  | `O(n^2)`           | **Quadratisch** - Die Komplexität verhält sich quadratisch zur Anzahl der Eingabewerte. Beispiel: Sortierverfahren wie BubbleSort oder Vergleich jedes Wertes mit jedem anderen| ```foreach (n1 in werte) { foreach(n2 in werte) { if(n1 == n2) ... } }``` |
|  | `O(n^k)`           | **Polynomial** - Ein Algorithmus, dessen Leistung proportional ist zum dem Quadrat der Größe des Datensatzes ist. Erhebliche Verringerung der Effizienz bei immer größeren Datensätzen. Tiefer geschachtelte Iterationen führen zu O(N3), O(N4), usw., je nach Anzahl der Dimensionen. | ```foreach (n1 in werte) foreach(n2 in werte) foreach(n3 in werte) sum += n1 + n2 + n3;``` |
|   | `O(2^n)` | **Exponential** - Ein Algorithmus, der sich mit jeder Hinzufügung zum Datensatz in jedem Durchgang verdoppelt. Im Gegensatz zum logarithmischen Algorithmus. Ineffizient. | ```Function fib(x) If x <= 1 Then Return x Return fib(x - 2) + fib(x - 1) End Function```  |

## Beispiel Codes pro Komplexitätsklasse

### Konstante Komplexität (O(1))

**Aufgabe:** Implementiere eine Funktion, die immer denselben Wert zurückgibt, unabhängig von der Eingabe.
**Code:** 
```C#
public double GetPi()
{
    return Math.Pi;
}
```

### **Logarithmische Komplexität (O(log(n)))**
**Aufgabe:** Implementiere eine Funktion, die eine Schleife enthält, die die Eingabegröße bei jedem Schritt halbiert.
**Code:** 
```C# 
void Procedure4(int n) {
    int j=n;
    while(j > 0) {
   	 j = j/2;
   	 do_something(i,j,n);
    }
}
```

### **Lineare Komplexität (O(n))**
**Aufgabe:** Implementiere eine Funktion, die die Anzahl der Elemente in einem Array zählt.
**Code:** 
```C#
public int GetCount(int[] array)
{
    int n = 0;
    foreach (int i in array)
        n++;
    return n;
}
```

### **Überlineare Komplexität (O(n log(n)))**
**Aufgabe:** Implementiere einen Sortieralgorithmus wie MergeSort.
**Code:** 
```C# 
public void MergeSort(int[] array) 
{ 
    /* MergeSort Implementation */ 
}
```

### **Quadratische Komplexität (O(n^2))**
**Aufgabe:** Implementiere eine Funktion, die jedes Element eines Arrays mit jedem anderen vergleicht.
**Code:** 
```C#
foreach (n1 in werte)
{
   foreach(n2 in werte)
   {
      if(n1 == n2) ...
}
```

### **Polynomiale Komplexität (O(n^k))**
**Aufgabe:** Implementiere eine Funktion, die drei verschachtelte Schleifen enthält, die alle Kombinationen von Elementen eines Arrays durchlaufen.
**Code:** 
```C#
foreach (n1 in werte)
   foreach(n2 in werte)
      foreach(n3 in werte)
         sum += n1 + n2 + n3;
```

