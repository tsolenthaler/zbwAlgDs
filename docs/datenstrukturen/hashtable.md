---
tags:
  - Hashtable
hide:
  #- navigation
  #- toc
---

# Hashtable

## Ziele

- [x] Ich wisse, was eine Hashtable ist
- [x] Ich wisse, was eine Hash-Funktion ist
- [ ] Ich kennen die Eigenschaften einer Hash-Funktion
- [ ] Ich wisse, wie mit Kollisionen beim Hinzufügen umgegangen werden kann

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
a) geschlossene Adressierung 
b) offene Adressierung 
c) Doppeltes Hashing 

b……. Bei einer Kollision wird einfach der nächste offene Platz gesucht. 
c……. Hierbei wird bei einer Kollision einen zweiten Hashwert berechnet. Das Resultat des zweiten Hashwertes entspricht dann den Anzahl Stellen um welche verschoben wird. 
a……. Bei einer Kollision werden weitere Objekte in einer verketteten Liste abgelegt. Diese Variante erfordert eine weitere Datenstruktur, was zusätzlicher Speicherverbrauch bedeutet.

### 2. Aufgabe 
Bestimmen Sie die Komplexitätsklasse einer Hashtable (für Add() sowie Remove(). Begründen Sie Ihre Antwort.

### 3. Aufgabe: 
Das Lineare Sondieren als Konfliktbehandlungsalgorithmus hat den Nachteil, dass es leicht zur Bildung 
von Clustern führt. Wie können Sie diesen Nachteil vermeiden?

### 4. Aufgabe
Gegeben sei folgende Hashtable, welche mit Hilfe der offenen Adressierung Konflikte beseitigt.  
Die Länge der Hashtable beträgt N = 7 
Die Hashfunktion sei index(k) = k % N 
Geben Sie nach jeder Operation die resultierende Hashtable an. 
Add(22) 
Add(3) 
Add(7) 
Add(14) 
Add(0) 
Remove(14) 

### 5. Aufgabe
Gegeben sei folgende Hashtable, welche mit Hilfe der offenen Adressierung Konflikte beseitigt. 
Diesmal wird die Schrittweite mittels einer zweiten Hashfunktion (Doppel-Hashing) berechnet.  
Die Länge der Hashtable beträgt N = 10 
Die Hashfunktion sei i𝑛𝑑𝑒𝑥(𝑘) = (k/100) % 𝑁 
Die Hashfunktion für die Schrittweite sei 𝑠𝑡𝑒𝑝𝑠(𝑖𝑛𝑑𝑒𝑥) = 7 −(𝑖𝑛𝑑𝑒𝑥 %7)

Geben Sie nach jeder Operation die resultierende Hashtable an. 

Add(1001)

Add(1542)

Add(429)

Add(1420)

Add(2116)

Add(1146)

Remove(2116)

Remove(1146)
