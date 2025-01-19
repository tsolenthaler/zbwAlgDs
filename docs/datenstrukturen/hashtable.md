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