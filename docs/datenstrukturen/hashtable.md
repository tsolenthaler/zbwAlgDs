---
tags:
  - Hashtable
hide:
  #- navigation
  #- toc
---

# Hashtable

### Übungen 

- **Promt:** 
    ```
    
    ```

## Übersicht

* Assoziatives Array - Speicherung von Key/Value Paaren
* Jeder Key ist eindeutig
* Der Key-Typ wird zu einem Index gemappt
* Bsp: Hashtable mit Personen
    * Hinzufügen von Jane
        * int index = GetIndex(Jane.Name)
        * _array[index] = Jane;


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
l = 108 = 01101100
o = 111 = 01101111
r = 114 = 01110010
e = 101 = 01100101

→ 01100101 01110010 01101111 01101100 = 1701998444

* Ein bisschen besser
    * String-Folding: Berechnet aus jeweils 4 Zeichen einen Integer
        * ASCII-Werte sind 1 Byte (8 Bits: 0-255)
        * Integer-Werte sind 4 Bytes (32Bits)
        ``` l|o|r|e|m| |i|p|s|um |d|o|l|o|r| ```

Zerteil in 4 Zeichen (Bytes):

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

    Was bedeutet uniform?? -->


### Werte zum Array hinzufügen

```C#
int arrayLength = 9;
int hashCode = GetHashCode(Jane.Name);
int index = hashCode % arrayLength;
_array[index] = Jane;
```

--> Kollisionen!

``` mermaid
flowchart TD
    1 2 3[Jane] 4 5 6 7 8 9
```

#### Kollisionen behandeln

* Zwei verschiedene Werte erhalten den gleichen Hashwert
    * Werte werden dem gleichen Index in der Hashtable zugewiesen
* Zwei verbreitete Strategien (Lesen Sie im Buch S. 87-90)
    * Verkettung
        * Speicherung der Werte in einer LinkedList
        * manchmal auch «geschlossene Adressierung» genannt
    * Offene Adressierung
        * Verschiebung zum nächsten freien Index
        * Manchmal «linear probing» bzw. «lineares Sondieren» genannt
        * Manchmal mittels «doppeltem Hashing»

##### Offene Adressierung

```C#
int arrayLength = 9;
int hashCode = GetHashCode(Jane.Name);
int index = hashCode % arrayLength;
while(_array[index] != null)
    index++;
_array[index] = Person;
```