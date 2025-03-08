---
tags:
  - komplexitätsklassen
  - o-notation
hide:
  #- navigation
  #- toc
---

# Performance von Algorithmen

## Ziele
- [x] Ich kennen die Problematik bzgl. Performancemessung von Algorithmen
- [x] Ich wisse, was mit asymptotischer Komplexität gemeint ist
- [x] Ich kann die Komplexitätsklasse von Algorithmen benennen
- [x] Ich kenne den Unterschied, zwischen Worst-Case- und Best-Case-Komplexität
- [x] Ich wisse, was die O Notation ist

## Komplexitätsklassen

![Komplexitätsklassen](https://images.squarespace-cdn.com/content/v1/5c5c91c1b7c92c593c4f65b1/1634157762557-YMNNZPL0011WZW1M2NW3/big-o-notation-graph.png){ align=left }

| #       | Komplexitätsklasse | Beschreibung | Beispiel |
| ------- | ------------------ | ------------ | -------- |
| 🟩 | `O(1)`             |  **Konstant** - Ein Algorithmus, der unabhängig von der Größe des Datensatzes immer in der gleichen Zeit ausführt, unabhängig von der Größe des Datensatzes. Effizient bei jedem Datensatz. | ```public double GetPi() { return Math.Pi; }``` |
| 🟩 | `O(log(n))`        | **Logarithmisch** - Ein Algorithmus, der den Datensatz in jedem Durchgang halbiert. Im Gegensatz zu exponentiell. Effizient bei großen Datensätzen. | ```void Procedure4(int n) { int j=n; while(j > 0) { j = j/2; do_something(i,j,n); } }``` |
| 🟨 | `O(n)`             | **Linear** - Ein Algorithmus, dessen Leistung mit wachsendem Datensatz abnimmt wächst. Reduziert die Effizienz bei immer größeren Datensätzen. | ```public int GetCount(int[] array) { int n = 0; foreach (int i in array) n++; return n; }``` |
| 🟧 | `O(n log(n))`      | **Überlinear** - Die Komplexität verhält sich loglinear zur Anzahl der Eingabewerte und liegt über der linearen Kurve. <br/>Beispiel: Sortalgorithmen wie MergeSort: <br/>- bei linearer Laufzeit verdoppelt sich die Laufzeit bei Verdoppelung der Eingabewerte <br/>- bei konstanter Laufzeit bleibt die Laufzeit bei Verdoppelung der Eingabewerte gleich <br/>- bei quadratischer Laufzeit steigt die Laufzeit bei Verdoppelung der Eingabewerte quadratisch an|  |
| 🟪 | `O(n^2)`           | **Quadratisch** - Die Komplexität verhält sich quadratisch zur Anzahl der Eingabewerte. Beispiel: Sortierverfahren wie BubbleSort oder Vergleich jedes Wertes mit jedem anderen| ```foreach (n1 in werte) { foreach(n2 in werte) { if(n1 == n2) ... } }``` |
| 🟥 | `O(n^k)`           | **Polynomial** - Ein Algorithmus, dessen Leistung proportional ist zum dem Quadrat der Größe des Datensatzes ist. Erhebliche Verringerung der Effizienz bei immer größeren Datensätzen. Tiefer geschachtelte Iterationen führen zu O(N3), O(N4), usw., je nach Anzahl der Dimensionen. | ```foreach (n1 in werte) foreach(n2 in werte) foreach(n3 in werte) sum += n1 + n2 + n3;``` |
| 🟥 | `O(2^n)` | **Exponential** - Ein Algorithmus, der sich mit jeder Hinzufügung zum Datensatz in jedem Durchgang verdoppelt. Im Gegensatz zum logarithmischen Algorithmus. Ineffizient. | ```Function fib(x) If x <= 1 Then Return x Return fib(x - 2) + fib(x - 1) End Function```  |

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

####  Komplexität bei Trees


| Baumtyp               | Einfügen          | Suchen            | Löschen           | In-Order Traversierung |
|----------------------|-------------------|-------------------|-------------------|------------------------|
| **Binärer Search Tree** | O(log n)          | O(log n)          | O(log n)          | O(n)                   |
|                      | O(n)              | O(n)              | O(n)              |                        |
| **AVL-Tree**         | O(log n)          | O(log n)          | O(log n)          |                        |
| **B-Tee**           | O(log n)          | O(log n)          | O(log n)          |                        |


## Antworten

### Was ist mit asymptotischer Komplexität gemeint?

Asymptotische Komplexität ist ein Konzept in der Informatik, das verwendet wird, um die Effizienz von Algorithmen zu analysieren, insbesondere in Bezug auf ihre Laufzeit oder den Speicherbedarf, wenn die Eingabedaten sehr groß werden. Sie beschreibt, wie sich die Laufzeit oder der Speicherbedarf eines Algorithmus verhält, wenn die Größe der Eingabe (oft als n bezeichnet) gegen unendlich geht.

Die asymptotische Komplexität wird häufig in drei Hauptkategorien unterteilt:

1. O-Notation (Big O): Diese Notation beschreibt die obere Schranke der Laufzeit oder des Speicherbedarfs eines Algorithmus. Sie gibt an, wie die Laufzeit im schlimmsten Fall wächst. Zum Beispiel bedeutet O(n2), dass die Laufzeit im schlimmsten Fall quadratisch zur Größe der Eingabe wächst.

2. Ω-Notation (Omega): Diese Notation beschreibt die untere Schranke der Laufzeit oder des Speicherbedarfs. Sie gibt an, wie die Laufzeit im besten Fall wächst. Zum Beispiel bedeutet Ω(n), dass die Laufzeit im besten Fall linear zur Größe der Eingabe wächst.

3. Θ-Notation (Theta): Diese Notation beschreibt die genaue Wachstumsrate der Laufzeit oder des Speicherbedarfs. Sie wird verwendet, wenn die obere und untere Schranke gleich sind. Zum Beispiel bedeutet Θ(nlogn), dass die Laufzeit sowohl im besten als auch im schlimmsten Fall asymptotisch gleich nlogn ist.

Die asymptotische Analyse hilft dabei, Algorithmen zu vergleichen und zu verstehen, wie sie sich verhalten, wenn die Eingabedaten wachsen, ohne sich um spezifische Implementierungsdetails oder konstante Faktoren kümmern zu müssen. Dies ist besonders nützlich, um die Skalierbarkeit von Algorithmen zu bewerten.

### Was ist der Unterschied, zwischen Worst-Case- und Best-Case-Komplexität?

Der Unterschied zwischen Worst-Case- und Best-Case-Komplexität bezieht sich auf die Analyse der Laufzeit oder des Speicherbedarfs eines Algorithmus unter verschiedenen Bedingungen der Eingabedaten. Hier sind die beiden Konzepte im Detail:

1. **Worst-Case-Komplexität**:
   - Die Worst-Case-Komplexität beschreibt die maximale Laufzeit oder den maximalen Speicherbedarf eines Algorithmus für die ungünstigsten Eingabewerte. 
   - Sie gibt an, wie lange ein Algorithmus im schlimmsten Fall benötigt, um ein Ergebnis zu liefern, unabhängig von der spezifischen Eingabe.
   - Diese Analyse ist wichtig, um sicherzustellen, dass der Algorithmus auch unter extremen Bedingungen effizient bleibt. 
   - Beispiel: Bei einem Sortieralgorithmus könnte die Worst-Case-Komplexität \( O(n^2) \) sein, was bedeutet, dass der Algorithmus im schlimmsten Fall quadratisch zur Anzahl der Elemente in der Liste läuft.

2. **Best-Case-Komplexität**:
   - Die Best-Case-Komplexität beschreibt die minimale Laufzeit oder den minimalen Speicherbedarf eines Algorithmus für die günstigsten Eingabewerte.
   - Sie gibt an, wie schnell ein Algorithmus im besten Fall ein Ergebnis liefern kann, wenn die Eingabe optimal ist.
   - Diese Analyse ist weniger häufig von Interesse, da sie oft nicht repräsentativ für die tatsächliche Leistung des Algorithmus ist, aber sie kann nützlich sein, um zu verstehen, wie der Algorithmus unter idealen Bedingungen funktioniert.
   - Beispiel: Bei einem Sortieralgorithmus könnte die Best-Case-Komplexität \( O(n) \) sein, wenn die Liste bereits sortiert ist.

Zusammenfassend lässt sich sagen, dass die Worst-Case-Komplexität die Leistung eines Algorithmus unter ungünstigen Bedingungen bewertet, während die Best-Case-Komplexität die Leistung unter optimalen Bedingungen bewertet. In der Praxis konzentrieren sich viele Analysen auf die Worst-Case-Komplexität, da sie eine realistischere Einschätzung der Leistung eines Algorithmus in den meisten Szenarien bietet.

### Was ist die O Notation?

Die O-Notation, auch als Big O-Notation bekannt, beschreibt die asymptotische Laufzeit oder den Speicherbedarf eines Algorithmus und gibt die obere Schranke der Laufzeit im schlimmsten Fall in Bezug auf die Größe der Eingabedaten an. Sie konzentriert sich auf das Wachstum der Laufzeit und ignoriert konstante Faktoren sowie niedrigere Ordnungsterme, um die Effizienz von Algorithmen zu vergleichen.

### Übungen 

- **Promt:** 
    ```
    Erstelle mir eine Aufgabe welche zufällig eine von diesen Komplexitätsklasse von O(1), O(n), O(log(n)), O(n log(n)), O(n^2) oder O(n^k) verwendet und ich die Komplexität bei einem C# Beispiel berechnen muss.
    ```