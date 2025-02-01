---
tags:
  - Hashtable
hide:
  #- navigation
  #- toc
---

# Hashtable

## Ziele

- [x] Ich weiss, was eine Hashtable ist
- [x] Ich weiss, was eine Hash-Funktion ist
- [ ] Ich kennen die Eigenschaften einer Hash-Funktion
- [ ] Ich weiss, wie mit Kollisionen beim Hinzufügen umgegangen werden kann

### Übungen 

- **Promt:** 
    ```
    Erstelle mir eine Aufgabe welche ich lösen muss und zum Thema Hashtabel und sich auf C# bezieht.
    ```

## Übersicht

* Assoziatives Array - Speicherung von Key/Value Paaren
* Jeder Key ist eindeutig
* Der Key-Typ wird zu einem Index gemappt
* Bsp: Hashtable mit Personen
    * Hinzufügen von Jane
```C#
int index = GetIndex(Jane.Name)
_array[index] = Jane;
```


### Hashing Übersicht
* Hashing erzeugt zu einem beliebigen Input einen Wert einer fixen Grösse und Typ (z.B. Int32)
* Stabil
    * Die gleiche Eingabe erzeugt jedes Mal den gleichen Hashwert
* Gleichmässig (uniform)
    * Hashwerte sollen gleichmässig über den verfügbaren Bereich verteilt sein
* Effizient
    * Die Hashfunktion soll effizient sein (in Bezug auf die Applikation)
* Sicher
    * Der Aufwand um zu einem Hashwert den Datenwert zu finden, soll so hoch sein, dass es «unmöglich» wird


### String Hashing

* Naive Implementierung
    * Additive: Summierung der ASCII-Werte von jedem Zeichen
    ``` foo --> 102|111|111 = 324 ```
    * Vorteile
        * Stabil
        * Effizient
    * Nachteile
        * Nicht gleichmässig: «foo» und «oof» ergeben den gleichen Hashwert
        * Nicht sicher
    
* Ein bisschen besser
    * String-Folding: Berechnet aus jeweils 4 Zeichen einen Integer
        * ASCII-Werte sind 1 Byte (8 Bits: 0-255)
        * Integer-Werte sind 4 Bytes (32Bits)

        ``` l|o|r|e|m| |i|p|s|um |d|o|l|o|r| ```

lorem -->

* l = 108 = 01101100
* o = 111 = 01101111
* r = 114 = 01110010
* e = 101 = 01100101

→ 01100101 01110010 01101111 01101100 = 1701998444

* Ein bisschen besser
    * String-Folding: Berechnet aus jeweils 4 Zeichen einen Integer
        * ASCII-Werte sind 1 Byte (8 Bits: 0-255)
        * Integer-Werte sind 4 Bytes (32Bits)
        ``` l|o|r|e|m| |i|p|s|um |d|o|l|o|r| ```

Zerteilt in 4 Zeichen (Bytes):

| Werte         | 'lore '    | 'm ip'     | 'sum '     | 'dolo'     | 'r   '        |
| -------       | -------    | ---------  | ---------- | --------   | --------      |
| ASCII-Werte   | 1701998444 | 1885937773 | 5440044403 | 1869377380 | 114           |
| Integer-Werte | 1701998444 | -707031079 | -162986676 | 1706390704 | 1706390818    |
               
* Vorteil:
    * Stabil, Effizient und besser gleichmässig verteilt

* Nachteil:
    * nicht sicher

### Hashing Functions

* Schreibe keine eigenen Hashing-Algorithmen!
* Wähle den richtigen Hash für die richtige Aufgabe

| Name          | Stable    | Uniform    | Efficient  | Secure       | 
| -------       | ------    | ---------  | ---------- | --------     | 
| Additive      | ✔️        | ❌        | ✔️           | ❌        |
| Folding       | ✔️        | ✔️        | ✔️           | ❌        |
| CRC32         | ✔️        | ✔️        | ✔️           | ❌        |
| MD5           | ✔️        | ✔️        | ❌           | ✔️        |
| SHA-2         | ✔️        | ✔️        | ❌           | ✔️        |

!!! question

    Was bedeutet uniform?? --> Hashwerte sollen gleichmässig über den verfügbaren Bereich verteilt sein.


### Werte zum Array hinzufügen

```C#
int arrayLength = 9;
int hashCode = GetHashCode(Jane.Name);
int index = hashCode % arrayLength;
_array[index] = Jane;
```

--> Kollisionen!


``` mermaid
flowchart LR
    1 ~~~ 2 ~~~ 3[Jane] ~~~ 4 ~~~ 5 ~~~ 6 ~~~ 7 ~~~ 8 ~~~ 9
```

#### Kollisionen behandeln

* Zwei verschiedene Werte erhalten den gleichen Hashwert
    * Werte werden dem gleichen Index in der Hashtable zugewiesen
* Zwei verbreitete Strategien (Lesen Sie im Buch S. 87-90)
    * Verkettung
    * Offene Adressierung


##### Offene Adressierung / linear probing / lineares Sondieren

* Verschiebung zum nächsten freien Index
* Manchmal «linear probing» bzw. «lineares Sondieren» genannt
* Manchmal mittels «doppeltem Hashing»

```C#
int arrayLength = 9;
int hashCode = GetHashCode(Jane.Name);
int index = hashCode % arrayLength;
while(_array[index] != null)
    index++;
_array[index] = Person;
```

``` mermaid
flowchart LR
    Steve --x 3
    Steve --> 4
    subgraph Array
        direction LR
        1 ~~~ 2 ~~~ 3[Jane] ~~~ 4 ~~~ 5 ~~~ 6 ~~~ 7 ~~~ 8 ~~~ 9
    end
```

##### Verkettung / geschlossene Adressierung

* Speicherung der Werte in einer LinkedList
* manchmal auch «geschlossene Adressierung» genannt

```C#
int arrayLength = 9;
int hashCode = GetHashCode(Jane.Name);
int index = hashCode % arrayLength;
_array[index].AddFirst(Person);
```

``` mermaid
flowchart LR
    subgraph Array
        direction LR
        1 ~~~ 2 ~~~ 3[Jane] ~~~ 4 ~~~ 5 ~~~ 6 ~~~ 7 ~~~ 8 ~~~ 9
    end
    3 --> Steve
```

#### Hashtable vergrössern

* Load Factor
    * Auslastung – sollte maximal 80% betragen
    * Auch bekannt als Füllgrad
* Add(item)

```C#
if(fillFactor >= maxFillFactor) {
    _newArray = new Array[_array.Length * 2];
    foreach(item in _array) {
        AddItemToHashTable(_newArray, item);
    }
    _array = newArray;
}
AddItemToHashTable(_array, newItem)
```

#### .NET GetHashCode()

* Wird von object implementiert
* Wenn nicht überschrieben, wird der HashCode von der Objektreferenz abgeleitet
* Wird verwendet, wenn das Objekt in eine Hashtable eingefügt wird
* Beispiel:

```C#
public class Person {
    public string Firstame { get; set; }
    public string Lastname { get; set; }
    public string Email { get; set; }

    public override int GetHashCode() {
        HashCode.Combine(this.Firstame, this.Lastname, this.Email);
    }
}
```

# Selbststudium

* Lesen Sie Kapitel 2.5 in Cordts2018, Lösen Sie die Aufgaben zum Kapitel (mindestens Aufgabe 1 und 2)
    * Errata: Bei Aufgabe 1 ist nicht «Methode HashtableLinearProbing» gemeint sondern «Klasse HashtableLinearProbing»
* Bearbeiten Sie das Beispiel in Cordts2018 (Beachten Sie auch die Quellcodes zum Buch – siehe Slides «Einführung»):
    * Maschinelle Lernverfahren – 1-Rule Klassifizierer (S. 97ff)


## Aufgaben

### 1. Aufgabe
Ordnen Sie folgende Begriffe der jeweils richtigen Definition zu: 

* a) geschlossene Adressierung 
* b) offene Adressierung 
* c) Doppeltes Hashing 

* b……. Bei einer Kollision wird einfach der nächste offene Platz gesucht. 
* c……. Hierbei wird bei einer Kollision einen zweiten Hashwert berechnet. Das Resultat des zweiten Hashwertes entspricht dann den Anzahl Stellen um welche verschoben wird. 
* a……. Bei einer Kollision werden weitere Objekte in einer verketteten Liste abgelegt. Diese Variante erfordert eine weitere Datenstruktur, was zusätzlicher Speicherverbrauch bedeutet.

### 2. Aufgabe 
Bestimmen Sie die Komplexitätsklasse einer Hashtable (für Add() sowie Remove(). Begründen Sie Ihre Antwort.

Add() = O(1)

Remove() = O(1)

Weil Array-Zugriffmechanik.

### 3. Aufgabe: 
Das Lineare Sondieren als Konfliktbehandlungsalgorithmus hat den Nachteil, dass es leicht zur Bildung 
von Clustern führt. Wie können Sie diesen Nachteil vermeiden?

In dem quadratisches Sondieren oder doppeltes Hashing (zweites Hashing) verwenden.

### 4. Aufgabe
Gegeben sei folgende Hashtable, welche mit Hilfe der offenen Adressierung Konflikte beseitigt.  

Die Länge der Hashtable beträgt N = 7 

Die Hashfunktion sei index(k) = k % N 

Geben Sie nach jeder Operation die resultierende Hashtable an.

Add(22) 

```22 % 7 = 1```

Mit Taschenrechner
```
22 / 7 = 3.1428571428571428571428571428571
3.1428571428571428571428571428571 - 3 = 0.14285714285714285714285714285714
0.14285714285714285714285714285714 * 7 = 1
```

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- |
|         | 22      |      |       |       |       |      |      |

Add(3)

3 % 7 = 3
Mit Taschenrechner
```
3 / 7 = 0.42857142857142857142857142857143
0.42857142857142857142857142857143 * 7 = 3
```

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- |
|         | 22      |      | 3     |       |       |      |      |

Add(7) 

7 % 7 = 0

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- |
| 7       | 22      |      | 3     |       |       |      |      |

Add(14) 

14 % 7 = 0

--> Index 0 und 1 ist besetzt, daher auf den nächsten freien Index 2

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- |
| 7       | 22      | 14   | 3     |       |       |      |      |

Add(0)

0 % 7 = 0

--> Index 0 besetzt, also auf den nächsten freien Index = 4

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- |
| 7       | 22      | 14   | 3     | 0     |       |      |      |

Remove(14) 

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- |
| 7       | 22      |      | 3     | 0     |       |      |      |

### 5. Aufgabe
Gegeben sei folgende Hashtable, welche mit Hilfe der offenen Adressierung Konflikte beseitigt. 
Diesmal wird die Schrittweite mittels einer zweiten Hashfunktion (Doppel-Hashing) berechnet.  

Die Länge der Hashtable beträgt N = 10 

Die Hashfunktion sei i𝑛𝑑𝑒𝑥(𝑘) = (k/100) % 𝑁 

Die Hashfunktion für die Schrittweite sei 𝑠𝑡𝑒𝑝𝑠(𝑖𝑛𝑑𝑒𝑥) = 7 −(𝑖𝑛𝑑𝑒𝑥 %7)

Geben Sie nach jeder Operation die resultierende Hashtable an. 

#### Add(1001)

index(1001)= (1001 / 100) % 10 = 10 % 10 = 0

Taschenrechner
```
1001 / 100 = 10.01
10.01 / 10 = 1.001
1.001 - 1 = 0.5
0.001 * 10 = 0.01 = 0
```

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    | 8    | 9     |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- | ---- | ---- |
| 1001    |       |      |      |      |      |      |      |       |       |

#### Add(1542)

index(1542)= (1542 / 100) % 10 = 15 % 10 = 5

Taschenrechner
```
1542 / 100 = 15.42
15.42 / 10 = 1.5
1.5 - 1 = 0.5
0.5 * 10 = 5
```

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    | 8    | 9     |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- | ---- | ---- |
| 1001    |       |         |      |      | 1542      |      |      |       |       |

#### Add(429)

index(429)= (429 / 100) % 10 = 4 % 10 = 4

Taschenrechner
```
429 / 100 = 4.29
4.29 / 10 = 0.429
0.429 * 10 = 4.29 = 4
```

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    | 8    | 9     |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- | ---- | ---- |
| 1001    |       |         |      | 429   | 1542  |      |      |       |       |

#### Add(1420)

index(1420)= (1420 / 100) % 10 = 14 % 10 = 4

steps(i)= 7 − (4 % 7 ) = 7 − 4 = 3

Taschenrechner --> bei % immer nach dem "." nehmen --> 1.4 --> 4

* 1.Schritt (1420 / 100) % 10
```
1420 / 100 = 14.2
14.2 / 10 = 1.42
1.42 * 10 = 14.2 = 14
```
* 2.Schritt - 14 % 10
```
14 / 10 = 1.42
1.42 - 1 = 0.42
0.42 * 10 = 4.2 = 4
```
* 4.Schritt Steps berechnen
7 − (4 % 7 )
```
4 / 7 = 0.57142857142857142857142857142857
0.57142857142857142857142857142857 * 7 = 4
```
7 - 4 = 3

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    | 8    | 9     |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- | ---- | ---- |
| 1001    |       |         |      | 429   | 1542  |      | 1420 |       |       |


#### Add(2116)

index(2116)= (2116 / 100) % 10 = 21 % 10 = 1

```
2116 / 100 = 21.16
21.16 / 10 = 2.116
2.116 * 10 = 21.16 = 21
```

```
21 / 10 = 2.116
2.116 - 2 = 0.11642
0.116 * 10 = 1.16 = 1
```

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    | 8    | 9     |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- | ---- | ---- |
| 1001    | 2116    |      |      | 429   | 1542  |      | 1420 |       |       |

#### Add(1146)

index(1146)= (1146 / 100) % 10 = 11 % 10 = 1

```
1146 / 100 = 11.46
11.46 / 10 = 1.146
1.146 * 10 = 11.46 = 11
```

```
11 / 10 = 1.1
1.1 - 1 = 0.1
0.1 * 10 = 1
```

7 − (1 % 7 )
```
1 / 7 = 0.14285714285714285714285714285714
0.14285714285714285714285714285714 * 7 = 1
```
7 - 1 = 6 Steps


--> 1 + 6 = Index 7 --> 7 ist belegt + 6 = Index 3 frei

* Suche nach freien Index "Formel"
    * Für i=0: index = ( 1 + 0 * 6 ) % 10 = 1 (belegt)
    * Für i=1: index = ( 1 + 1 * 6 ) % 10 = 7 (belegt)
    * Für i=2: index = ( 1 + 2 * 6 ) % 10 = 3 (leer)

| Index 0 |  1      | 2    | 3     | 4     | 5     | 6    | 7    | 8    | 9     |
| ------- | -----   | ---  | ----- | ----- | ----  | ---- | ---- | ---- | ---- |
| 1001    | 2116    |      | 1146  | 429   | 1542  |      | 1420 |       |       |

Remove(2116)

--> selbe Berechnung für Position / Index

Remove(1146)

--> selbe Berechnung für Position / Index