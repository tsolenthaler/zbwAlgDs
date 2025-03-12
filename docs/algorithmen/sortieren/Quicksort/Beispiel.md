# Beispiel Quicksort
```
teile(links, rechts)
```

Die Buchstabenfolge „einbeispiel“ soll alphabetisch sortiert werden.

Ausgangssituation nach Initialisierung von i und j, das Element rechts (l) ist das Pivotelement:

```
e i n b e i s p i e l
^                 ^
i                 j
```

Nach der ersten Suche in den inneren Schleifen hat i auf einem Element > l und j auf einem Element <= l gehalten:

```
e i n b e i s p i e l
  ^             ^
  i             j
```

Nach dem Tauschen der Elemente bei i und j:

```
  e i e b e i s p i n l
      ^             ^
      i             j
```

Nach der nächsten Suche und tauschen:
```
  e i e b e i i p s n l
              ^   ^
              i   j
```

Nach einer weiteren Suche sind die Indizes aneinander vorbeigelaufen:
```
  e i e b e i i p s n l
              ^ ^
              j i
```

Nach dem Tauschen von i und Pivot bezeichnet i die Trennstelle der Teillisten. Bei i steht das Pivot-Element, links davon sind nur Elemente ≤ Pivot und rechts nur solche > Pivot:
```
  e i e b e i i l s n p
                ^
                i
```

## Vollständiges Beispiel für alphabetische Sortierung

In diesem Beispiel soll der Quicksortalgorithmus die Buchstabenfolge „Quicksort“ sortieren. Zunächst wird das rechte Element P-> als Pivotelement definiert. Dann laufen die Zähler g für „größer“ von links nach rechts und k für „kleiner“ von rechts nach links los,

```
 Quicksort
^       ^^
g       kP
```

bis g auf ein Element trifft, welches größer als das Pivotelement ist und bis k auf ein Element trifft, welches kleiner oder gleich dem Pivotelement ist.
```
 Quicksort
  ^     ^^
  g     kP
```
Diese beiden gefundenen Elemente r und u werden dann im folgenden Schritt getauscht.
```
 Qricksout
  ^     ^^
  g     kP
```
Im folgenden Schritt laufen die Indizes k und g in der gleichen Richtung wie gehabt weiter und suchen Elemente, die bei k kleiner als oder gleich dem Pivotelement und bei g größer als das Pivotelement sind.
```
 Qricksout
       ^^^
       kgP
```
Jetzt sind k und g aneinander vorbeigelaufen. Dieses Ereignis ist eine Abbruchbedingung. Jetzt wird das Pivotelement mit dem durch g indizierten Element getauscht.
```
 Qricksotu
       ^^^
       kPg
```
Jetzt treffen folgende zwei Aussagen zu: „Links des Pivotelements sind alle Elemente kleiner oder gleich dem Pivotelement. Rechts des Pivotelements sind alle Elemente größer oder gleich dem Pivotelement.“
```
   links|:|rechts
 Qrickso|t|u
       ^|^|^
       k|P|g
```
Das Pivotelement „teilt“ nun die Datenmenge an der Stelle des Pivotelements in zwei Hälften Links und Rechts. Nun muss der Algorithmus den linken und den rechten Teil auf die gleiche Weise wie im Vorangehenden schon geschehen weiterbehandeln. Hierdurch ergibt sich nun die Rekursion. Der rechte Teil (Der Buchstabe u) ist nur ein einzelnes Element und ist somit per Definition sortiert. Also wird nun der linke Teil behandelt. Das rechte Element ist wieder das Pivotelement, und die Zähler werden passend gesetzt.
```
 Qrickso|t|u
^     ^^
g     kP
```
Das Q ist größer als o und das k ist kleiner als das o.
```
 Qrickso|t|u
 ^   ^ ^
 g   k P
```
Also werden das Q und das k vertauscht.
```
 kricQso|t|u
 ^   ^ ^
 g   k P
```
Indizes g und k laufen weiter...
```
 kricQso|t|u
  ^ ^  ^
  g k  P
```
Das r und das c werden getauscht.
```
 kcirQso|t|u
  ^ ^  ^
  g k  P
```
Im folgenden Schritt sind die Indizes wieder aneinander vorbeigelaufen...
```
 kcirQso|t|u
   ^^  ^
   kg P
```
… und das Pivotelement (Buchstabe o) wird mit dem größeren Element (Buchstabe r) getauscht.
```
 kcioQsr|t|u
   ^^  ^
   kP  g
```
Nun ergibt sich erneut ein linker und ein rechter Teil.
```
links:rechts
 kci|o|Qsr  |t|u
   ^|^|  ^  | |
   k|P|  g  | |
```
Zunächst wird der linke Teil behandelt.
```
 kci|o| Qsr|t|u
^ ^^| |^ ^^| |
g kP| |g kP| |
```
```
 cki|o| Qsr|t|u
 ^^^| |^ ^^| |
 gkP| |g kP| |
```
Buchstabe c und k werden getauscht.
```
 cki|o| Qsr|t|u
 ^^^| |^ ^^| |
 kgP| |g kP| |
```
Indizes sind aneinander vorbeigelaufen, und das Element des Index g wird mit dem des Index P vertauscht.
```
 cik|o| Qsr|t|u
 ^^^| |^ ^^| |
 kPg| |g kP| |
```
Der jetzt entstandene neue linke und rechte Teil besteht nun nur noch aus einem einzelnen Element und gilt als sortiert.
```
 cik|o| Qsr|t|u
    | | ^^^| |
    | | kgP| |
```
Im ehemals rechten Teil (Buchstaben Qsr) laufen die Indizes direkt aneinander vorbei, und das Element bei g wird mit dem Pivotelement getauscht.
```
 cik|o| Qrs|t|u
    | | ^^^| |
    | | kPg| |
```
Damit sind alle Zeichen sortiert.
```
 cik|o| Qrs|t|u
```
Ergebnis:
```
 cikoQrstu
```