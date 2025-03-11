# B-Tree

## Ziele

- [x] Ich kenne den Unterschied zwischen einem BinaryTree und einem B-Tree
- [ ] Ich weiss, wie die Operationen «Einfügen» und «Löschen» auf einen B-Tree angewendet werden

## Motivation

Die Verwendung von AVL-Trees für die Indexierung der Datenbank könnte zwar eine ausgeglichene Baumstruktur und effiziente Suchoperationen in Theorie gewährleisten, aber bei jeder Einfügung oder Löschung von Daten müssten möglicherweise mehrere Rotationen durchgeführt werden, um den Baum auszugleichen. Dies ist insbesondere problematisch, wenn die Datenbank auf einem Festplattenspeicher liegt, da jede Änderung im Baum zu potenziell vielen Plattenzugriffen führen kann, um die betroffenen Knoten zu lesen oder zu schreiben. Da Plattenzugriffe im Vergleich zu Operationen im Arbeitsspeicher sehr langsam sind, könnten die Wartungskosten des AVL-Trees in einer solchen Umgebung sehr hoch werden.

## Übersicht

* Erfunden von Rudolf Bayer und Edward M. McCreight 1972 für die Verwaltung von Indizes in relationalen Datenbanken (erfunden von Edgar F. Codd 1970)
* Keine Erklärung für Herkunft des Namens. Interpretation: B für balanciert, Bayer, Barbara (Frau von Bayer), Boeing (Bayer arbeitete für Boeing Scientific Research)
* kleiner als ">1" 1 Key pro Node
* ≥ 2 Child Nodes
* Self-Balancing
* Grössere Verzweigungsgrad reduziert die Baumhöhe und somit die Anzahl Lesezugriffe
* Variable Schlüsselmenge pro Node vermeidet häufiges Balancing

## Eigenschaften
* Jede Page enthält höchstens 2𝑑 Keys (Elemente)
* Jede Page, ausser Root, enthält mindestens 𝑑 Keys
* Root hat min. 1 und max. 2𝑑 Keys
* Jede Page ist entweder Leaf, d.h. hat keine Childs oder sie hat 𝑚 + 1 Childs, wobei 𝑚 die Anzahl ihrer Keys ist
* Die Keys einer Page sind aufsteigend sortiert
* Alle Leafs liegen auf der gleichen Stufe
* Wie bei Binary Search Tree: Links → kleiner, rechts → grösser oder gleich

``` mermaid
flowchart TD
    1[34]
    1 --> 2[12 29]
    1 --> 3[46 67]
    2 --> 4[2 8 9 10]
    2 --> 5[15 19 22 24]
    2 --> 6[30 31 32]
    3 --> 7[36 39]
    3 --> 8[53 57 63 65]
    3 --> 9[72 83 94 96]
```


##  Unterschied zwischen einem BinaryTree und einem B-Tree

### Binary Tree (Binärbaum)

* Struktur: Ein Binärbaum ist eine Baumstruktur, in der jeder Knoten höchstens zwei Kinder hat, die als linkes und rechtes Kind bezeichnet werden.

* Knoten: Jeder Knoten im Binärbaum enthält einen Wert und Verweise auf seine beiden Kinder (linkes und rechtes Kind).

* Anwendung: Binärbäume werden häufig in der Informatik verwendet, z.B. in Suchbäumen (wie dem Binären Suchbaum), um Daten effizient zu speichern und zu durchsuchen.

* Balancierung: Binärbäume können unausgewogen sein, was zu einer schlechten Leistung bei Suchoperationen führen kann. Es gibt jedoch balancierte Varianten wie AVL-Bäume oder Rot-Schwarz-Bäume.

* Zugriffszeit: Die Zugriffszeit kann im schlimmsten Fall O(n) betragen, wenn der Baum unausgewogen ist.

### B-Tree

* Struktur: Ein B-Tree ist eine selbstbalancierende Baumstruktur, die für die Speicherung von Daten in einer Datenbank oder auf Festplatten optimiert ist. Jeder Knoten kann mehrere Kinder haben (mindestens zwei und maximal eine bestimmte Anzahl, die als Ordnung des Baums bezeichnet wird).

* Knoten: Jeder Knoten in einem B-Tree kann mehrere Werte und Verweise auf seine Kinder enthalten. Die Werte in einem Knoten sind sortiert, und die Kinder sind so angeordnet, dass alle Werte im linken Kind kleiner und alle Werte im rechten Kind größer sind.

* Anwendung: B-Bäume werden häufig in Datenbanken und Dateisystemen verwendet, da sie eine effiziente Speicherung und Suche von Daten ermöglichen, insbesondere bei großen Datenmengen, die nicht vollständig im Hauptspeicher gehalten werden können.

* Balancierung: B-Bäume sind immer balanciert, was bedeutet, dass alle Blätter auf der gleichen Ebene sind. Dies sorgt für eine gleichmäßige Verteilung der Daten und eine konsistente Zugriffszeit.

* Zugriffszeit: Die Zugriffszeit ist logarithmisch in Bezug auf die Anzahl der gespeicherten Elemente, typischerweise O(log n), was sie effizienter macht als unausgewogene Binärbäume.

### Zusammenfassung

* Binärbaum: Jeder Knoten hat maximal zwei Kinder, kann unausgewogen sein, wird häufig für Suchoperationen verwendet.
* B-Tree: Jeder Knoten kann mehrere Kinder haben, ist immer balanciert, optimiert für Datenbanken und große Datenmengen.

## wie werden die Operationen «Einfügen» und «Löschen» auf einen B-Tree angewendet?
Ein B-Baum ist eine selbstbalancierende Datenstruktur, die in der Informatik häufig für Datenbanken und Dateisysteme verwendet wird. Die Operationen „Einfügen“ und „Löschen“ in einem B-Baum sind so gestaltet, dass die Eigenschaften des Baums erhalten bleiben. Hier sind die grundlegenden Schritte für beide Operationen:

### Einfügen in einen B-Baum

1. **Finde die richtige Position**: Beginne an der Wurzel und gehe rekursiv nach unten, um die richtige Blattposition für den neuen Schlüssel zu finden. Vergleiche den neuen Schlüssel mit den vorhandenen Schlüsseln, um zu entscheiden, in welchen Kindknoten du weitergehen sollst.

2. **Füge den Schlüssel ein**: Wenn du ein Blatt erreicht hast, füge den neuen Schlüssel in den Blattknoten ein. Die Schlüssel im Knoten müssen in sortierter Reihenfolge bleiben.

3. **Überlauf behandeln**: Wenn der Knoten nach dem Einfügen mehr Schlüssel enthält als die maximale Anzahl (d.h. der Knoten überläuft):
   - Teile den Knoten in zwei Knoten. Der Medianwert wird nach oben in den übergeordneten Knoten verschoben.
   - Wenn der übergeordnete Knoten ebenfalls überläuft, wiederhole den Teilungsprozess rekursiv nach oben.

### Löschen aus einem B-Baum

1. **Finde den Schlüssel**: Beginne an der Wurzel und gehe rekursiv nach unten, um den Schlüssel zu finden, den du löschen möchtest.

2. **Löschen des Schlüssels**:
   - **Fall 1**: Der Schlüssel befindet sich in einem Blattknoten. Lösche den Schlüssel einfach.
   - **Fall 2**: Der Schlüssel befindet sich in einem inneren Knoten. Finde den Vorgänger (den größten Schlüssel im linken Teilbaum) oder den Nachfolger (den kleinsten Schlüssel im rechten Teilbaum), ersetze den zu löschenden Schlüssel durch diesen und lösche dann den Vorgänger oder Nachfolger (dies wird ein Blattknoten sein oder einen weiteren Fall auslösen).
   
3. **Unterlauf behandeln**: Nach dem Löschen kann es sein, dass ein Knoten weniger Schlüssel hat als die minimale Anzahl (d.h. der Knoten unterläuft):
   - Wenn möglich, leihe einen Schlüssel von einem Geschwisterknoten (links oder rechts).
   - Wenn das nicht möglich ist, führe eine Zusammenführung durch: Kombiniere den Knoten mit einem Geschwisterknoten und verschiebe einen Schlüssel vom übergeordneten Knoten nach unten.

### Eigenschaften des B-Baums

- Jeder Knoten hat eine bestimmte Anzahl von Schlüsseln, die zwischen einem Minimum und Maximum liegen.
- Alle Blätter befinden sich auf derselben Ebene.
- Der Baum bleibt nach jeder Einfüge- oder Löschoperation balanciert.

Diese Schritte gewährleisten, dass der B-Baum seine Struktur und Eigenschaften beibehält, während Schlüssel hinzugefügt oder entfernt werden.

## Aufgabe

* Berechnen Sie die max. Anzahl Keys, die in einem Baum 2. Ordnung (d.h. d=2) und h=3 gespeichert werden können.
* Tipp: Überlegen Sie sich, wieviele Keys in einem BinaryTree gespeichert werden können und versuchen Sie, Ihre Überlegungen zum oben spezifizierten B-Trees zu transferieren.

### Antwort
Ein B-Baum der Ordnung \( d \) hat die folgenden Eigenschaften:

1. Jeder Knoten kann maximal \( 2d \) Kinder haben.
2. Jeder Knoten kann maximal \( 2d - 1 \) Schlüssel enthalten.
3. Jeder Knoten (außer der Wurzel) muss mindestens \( d \) Kinder haben, wenn er nicht ein Blattknoten ist.
4. Die Höhe des Baums ist \( h \).

Für einen B-Baum der Ordnung \( d = 2 \) und Höhe \( h = 3 \) können wir die maximale Anzahl der Schlüssel wie folgt berechnen:

1. **Maximale Anzahl der Kinder pro Knoten**: Da \( d = 2 \), kann jeder Knoten maximal \( 2d = 4 \) Kinder haben.
2. **Maximale Anzahl der Schlüssel pro Knoten**: Jeder Knoten kann maximal \( 2d - 1 = 3 \) Schlüssel enthalten.

Jetzt betrachten wir die Struktur des Baums:

- **Ebene 0 (Wurzel)**: 1 Knoten, der maximal 3 Schlüssel enthalten kann.
- **Ebene 1**: Die Wurzel kann maximal 4 Kinder haben, also 4 Knoten. Jeder dieser Knoten kann maximal 3 Schlüssel enthalten, also insgesamt \( 4 \times 3 = 12 \) Schlüssel.
- **Ebene 2**: Jeder der 4 Knoten auf Ebene 1 kann ebenfalls maximal 4 Kinder haben, also insgesamt \( 4 \times 4 = 16 \) Knoten. Jeder dieser Knoten kann maximal 3 Schlüssel enthalten, also insgesamt \( 16 \times 3 = 48 \) Schlüssel.

Jetzt addieren wir die maximalen Schlüssel aus allen Ebenen:

- Ebene 0: 3 Schlüssel
- Ebene 1: 12 Schlüssel
- Ebene 2: 48 Schlüssel

Die maximale Anzahl der Schlüssel in einem B-Baum der Ordnung 2 und Höhe 3 ist also:

\[
3 + 12 + 48 = 63
\]

Somit kann ein B-Baum der Ordnung 2 und Höhe 3 maximal **63 Schlüssel** speichern.

## Einfügen

* Keys werden immer in Leafs eingefügt
* Beispiel (𝑑 = 2):

``` mermaid
flowchart TD
    A[32]
    A --> B[9 12 23 27]
    A --> C[33 45 54 67]
```

Einfügen 36

``` mermaid
flowchart TD
    A[32 45]
    A --> B[9 12 23 27]
    A --> C[33 36]
    A --> D[54 67]
```


* 36 wird in Page C eingefügt: (33,36,45,54,67) → Overflow
* Der Node wird aufgeteilt und das mittlere Element (45) nach oben gezogen
* Nun muss Page A bzgl. Overflow geprüft werden → i.O.


## Löschen
* zwei Fälle
    * Das zu löschende Element liegt auf Leaf → trivial
    * Element liegt nicht auf Leaf – das zu löschende Element wird durch das nächstgrössere (nächstkleinere) Element ersetzt. Dieses liegt immer auf Leaf (Suche analog BinarySearchTree)
* Beide Fälle erfordern eine Prüfung der Regel: min. 𝑑 Elemente Enthält die Page P durch Entfernen weniger als d Elemente, so werden die Elemente der Page P und der benachbarten Page Q gleichmässig auf beide Pages verteilt (ausbalanciert)

``` mermaid
flowchart TD
    A[32 45]
    A --> B[9 12 23]
    A --> C[33 36]
    A --> D[54 67 86]
```

Element 36 löschen

``` mermaid
flowchart TD
    A[32 54]
    A --> B[9 12 23]
    A --> C[33 45]
    A --> D[67 86]
```

* Wenn kein Element zum Angliedern vorhanden (d.h. P und Q enthalten 2𝑑 − 1 Elemente)
    * Page P und Q werden zusammengelegt und Element wird von Parent runtergezogen (Gegenteil von Einfügen)

``` mermaid
flowchart TD
    A[32 54]
    A --> B[9 12 23]
    A --> C[33 45]
    A --> D[67 86]
```

Element 45 löschen

``` mermaid
flowchart TD
    A[32]
    A --> B[9 12 23]
    A --> C[33 54 67 86]
```


* Das runterziehen kann die Grösse ebenfalls unter d sinken lassen
    * gleiche Aktion wird für diese Page wiederholt
    * kann sich bis zum Root fortsetzen


## Selbststudium

* B-Tree
    * https://en.wikipedia.org/wiki/B-tree
        * Wichtig: die englische Variante verwenden – die deutsche Variante verwendet eine andere Definition des B-Tree’s

### Hilfe

[B-Tree](https://studyflix.de/informatik/b-baum-1435)


### Unterschied

* Binärbaum: Jeder Knoten hat maximal zwei Kinder, kann unterschiedliche Strukturen haben und ist oft einfacher, aber weniger effizient bei großen Datenmengen.

* B-Baum: Jeder Knoten kann mehrere Schlüssel und Kinder haben, ist selbstbalancierend und optimiert für die Speicherung und den Zugriff auf große Datenmengen, insbesondere in externen Speichersystemen


### Regel

* von unten nach oben
* Varbiable Anzahl Key pro Blatt (bspw. 2, 4) Begrenzung = minimum 2, maximal 4 Element pro Blatt.
* Maximale Anzahl an Verweisen = Verzweigungsgrad oder Ordnung --> Verzweigungsgrad - 1 Eleme t
    * Machmal auch "Ordnung = maxiamle Anzahl an Elementen pro Knoten"


#### Beispiel

##### B-Baum der Ordnung 4

``` 
20, 50, 70
```

###### Einfügen von 35

``` 
20, 35, 50, 70
```

* --> Ordnung 4 wird überschritten
* aufteilen

```
    35
    / \
   20  50, 70
``` 

###### Löschen von 15

```
        20,50
    /     |      \
5,10,15  30,40   55,66,77
``` 

* Ordnung wird nicht verletzt.

```
        20,50
    /     |      \
5,10    30,40   55,66,77
``` 

###### Löschen von 40

```
        20,50
    /     |      \
5,10    30    55,66,77
``` 

* Ordnung wird verletzt
* verschieben
    * 55 nach oben
    * 50 zu mitteleren Blatt

```
        20,55
    /     |    \
5,10    30,50  66,77
``` 

###### Löschen von 50

```
        20,55
    /     |    \
5,10    30    66,77
``` 

* Ordnung wieder verletzt
* Knoten verschmelzen
    * 55 zu rechten Blatt
    * 30 zu rechten Blatt

```
       20
    /      \
5,10    30,55,66,77
``` 

##### Löschen von inneren Knoten - Löschen von 20

```
                  30
            /         \
        10,20        40,50
    /     |       \
  3,7  12,15,17   23,25
``` 

* Nur mittlere Knoten 12,15,17, da aus 3 Elmenten besteht.

* Regel
    * Linker Nachfolger: grösstes Element --> bspw. 17
        * Der mittlere Knoten ist der Linke Nachfolger der 20. Also wir die 17 (grösstes Element) genommen.
    * Rechter Nachfolger: kleinstes Element

```
                  30
            /         \
        10,17        40,50
    /     |       \
  3,7  12,15    23,25
``` 

###### Löschen von 17
```
                  30
            /         \
        10,17        40,50
    /     |       \
  3,7  12,15    23,25
``` 

* verschmelzen

```
                  30
            /         \
        10        40,50
    /     |       
  3,7  12,15,23,25
``` 

* Fehlt noch ein Element im Knoten mit 10.
* Rechter Nachfolger --> kleinstes Element 12 hochziehen

```
                  30
            /         \
        10,12        40,50
    /     |       
  3,7  15,23,25
``` 