# Insertionsort

* Stabil
* Prinzip: Sortieren durch Einfügen
* Laufzeit: 
    * Abhängig von:
        * Anzahl verschiebungen
        * Anordnung der Element
    * Average Case - O(n^2)
    * Worst Case - O(n^2)
    * Bet-Case - O(n) --> Liste ist Vorsortiert

## Beschreibung
Insertionsort (auch Sortieren durch Einfügen, englisch insertion ‚das Einfügen‘ und englisch sort ‚sortieren‘) ist ein einfaches stabiles Sortierverfahren (d. h., die Reihenfolge von Elementen mit gleichem Schlüsselwert bleibt unverändert). Es ist leicht zu implementieren, effizient bei kleinen oder bereits teilweise sortierten Eingabemengen. Außerdem benötigt Insertionsort keinen zusätzlichen Speicherplatz, da der Algorithmus in-place arbeitet. Ein weiterer Vorteil besteht darin, dass Insertionsort als Online-Algorithmus eingesetzt werden kann.

Der Insertionsort entnimmt der unsortierten Eingabefolge ein beliebiges Element und fügt es an richtiger Stelle in die (anfangs leere) Ausgabefolge ein. Geht man hierbei in der Reihenfolge der ursprünglichen Folge vor, so ist das Verfahren stabil. Wird auf einem Array gearbeitet, so müssen die Elemente hinter dem neu eingefügten Element verschoben werden. Dies ist die eigentlich aufwendige Operation des Insertionsorts. Das Auffinden der richtigen Einfügeposition kann über eine binäre Suche vergleichsweise effizient erfolgen. Grundsätzlich gilt aber, dass Insertionsort weit weniger effizient arbeitet als andere anspruchsvollere Sortierverfahren. 

## Problembeschreibung

Das Vorgehen ist mit der Sortierung eines Spielkartenblatts vergleichbar. Am Anfang liegen die Karten des Blatts verdeckt auf dem Tisch. Die Karten werden nacheinander aufgedeckt und an der korrekten Position in das Blatt, das in der Hand gehalten wird, eingefügt. Um die Einfügestelle für eine neue Karte zu finden, wird entweder die Karte sukzessive (von links nach rechts) mit den bereits einsortierten Karten des Blattes verglichen, oder eine binäre Suche durchgeführt. Zu jedem Zeitpunkt sind die Karten in der Hand sortiert und bestehen aus den bereits vom Tisch entnommenen Karten. Zum Einfügen der neuen Karte müssen alle auf der Hand nachfolgenden eine Position weiter nach rechts wandern.
Eingabe

Eine Folge von n zu sortierenden Zahlen ( a 1 , a 2 , … , a n ).

Die Zahlen werden auch als Schlüssel (keys) bezeichnet; diese sind oft nur ein Bestandteil eines Datensatzes. 

## Vorteile von Insertionsort:

* Einfachheit der Implementierung: Insertionsort ist leicht zu verstehen und zu implementieren, was es zu einer guten Wahl für einfache Sortieraufgaben macht.
* Stabilität: Das Verfahren ist stabil, d.h. die Reihenfolge von Elementen mit gleichem Schlüsselwert bleibt unverändert.
* Effizienz bei kleinen oder teilweise sortierten Daten: Insertionsort ist besonders effizient, wenn die Eingabemenge klein oder bereits teilweise sortiert ist. In solchen Fällen kann die Laufzeit deutlich unter O(n²) liegen.
* In-Place-Sortierung: Der Algorithmus benötigt keinen zusätzlichen Speicherplatz, da er in-place arbeitet, was bedeutet, dass die Sortierung direkt im ursprünglichen Array erfolgt.
* Online-Algorithmus: Insertionsort kann als Online-Algorithmus verwendet werden, was bedeutet, dass es Elemente sortieren kann, während sie eintreffen.

## Nachteile von Insertionsort:

* Ineffizienz bei großen Datenmengen: Im Vergleich zu anderen, komplexeren Sortierverfahren (wie Quicksort, Mergesort oder Heapsort) ist Insertionsort weniger effizient, insbesondere bei großen unsortierten Datenmengen, da die durchschnittliche und schlechteste Laufzeit O(n²) beträgt.
* Hohe Anzahl an Vergleichen und Verschiebungen: Die Anzahl der Vergleiche und Verschiebungen hängt stark von der Anordnung der Elemente ab. Im schlechtesten Fall (z.B. bei einem absteigend sortierten Array) sind viele Verschiebungen erforderlich, was die Leistung beeinträchtigt.
* Schwierige Abschätzung der Laufzeit im Durchschnittsfall: Die Laufzeit im Durchschnittsfall ist schwer genau abzuschätzen, was die Vorhersagbarkeit der Leistung des Algorithmus einschränkt.

## Anwendung

### Einsatzbereiche von Insertionsort:

* Kleine Datensätze: Insertionsort ist besonders effizient bei kleinen Datensätzen. Bei einer geringen Anzahl von Elementen (z. B. weniger als 20) kann Insertionsort schneller sein als komplexere Algorithmen, da die konstanten Faktoren und die einfache Implementierung den Overhead der anderen Algorithmen überwiegen.

* Teilweise sortierte Daten: Wenn die Eingabedaten bereits teilweise sortiert sind, kann Insertionsort sehr schnell arbeiten, da es in solchen Fällen weniger Vergleiche und Verschiebungen benötigt. In der besten Fall-Situation (bereits sortiert) hat der Algorithmus eine lineare Laufzeit von O(n).

* Echtzeit- oder Online-Anwendungen: Insertionsort kann in Szenarien eingesetzt werden, in denen Daten kontinuierlich eintreffen und sofort sortiert werden müssen. Da es als Online-Algorithmus funktioniert, kann es neue Elemente sofort in die bereits sortierte Liste einfügen.

* Stabile Sortierung erforderlich: In Anwendungen, in denen die Stabilität der Sortierung wichtig ist (d.h. die relative Reihenfolge von gleichwertigen Elementen beibehalten werden muss), ist Insertionsort eine geeignete Wahl.

* Einfache Implementierung: In Lehr- und Lernkontexten wird Insertionsort häufig verwendet, um grundlegende Konzepte der Sortierung und Algorithmen zu vermitteln, da es einfach zu verstehen und zu implementieren ist.

### Abgrenzung von Insertionsort:

* Große Datensätze: Bei großen Datensätzen ist Insertionsort in der Regel ineffizient, da seine durchschnittliche und schlechteste Laufzeit O(n²) beträgt. In solchen Fällen sind Algorithmen wie Quicksort, Mergesort oder Heapsort vorzuziehen, die eine bessere Leistung bieten.

* Komplexe Datenstrukturen: In Anwendungen, die komplexe Datenstrukturen oder große Mengen an Daten erfordern, sind fortgeschrittene Sortieralgorithmen, die auf Divide-and-Conquer-Strategien basieren, oft die bessere Wahl.

* Häufige Sortieroperationen: Wenn häufige Sortieroperationen auf großen Datenmengen erforderlich sind, sind Algorithmen, die eine bessere durchschnittliche Laufzeit bieten, wie Mergesort oder Heapsort, geeigneter.

* Nicht-stabile Sortierung: In Fällen, in denen die Stabilität der Sortierung nicht erforderlich ist, können andere Algorithmen, die möglicherweise schneller sind, bevorzugt werden.

## Impelmentierung

### Pseudocode

Der folgende Pseudocode sortiert die Eingabefolge aufsteigend. Um eine absteigende Sortierung zu erreichen, ist der zweite Vergleich in Zeile 4 entsprechend zu ändern. Der Parameter A ist ein Feld mit der zu Beginn unsortierten Folge. Nach Beendigung des Algorithmus enthält A mit den Elementen A[0], A[1], …, A[n-1] die sortierte Folge.

Hierbei ist zu beachten, dass die Indizierung des Feldes mit einer 0 beginnt.

n : Anzahl der Elemente von A

n − 1 : Index des letzten Elementes von A

```
INSERTIONSORT(A)

for i = 1 to (Länge(A)-1) do
     einzusortierender_wert = A[i]
     j = i
     while (j > 0) and (A[j-1] > einzusortierender_wert) do
          A[j] = A[j - 1]
          j = j - 1
     end while
     A[j] = einzusortierender_wert
end for
```

Anmerkungen:

* Die Positionsvariable i kann bei 1 beginnen anstatt bei 0, da ein Sortieren erst beginnt, wenn wenigstens zwei Werte gegeben sind (i=0 und i=1), erst dann kommt es zum ersten Vergleich. Davor kann A[0] als „bereits sortiert“ betrachtet werden.
* Die innere j-while-Schleife verschiebt im bereits sortierten Bereich 0..(i-1) alle „zu große“ Elemente eine Position nach hinten. Dadurch ergibt sich an richtiger Stelle dann der eine Freiraum, um den einzusortierenden Wert einzufügen.

### Struktogramm

Im Folgenden ein Nassi-Shneiderman-Diagramm (Struktogramm) des Insertionsort-Algorithmus. Die Bezeichner sind an obigen Pseudocode angelehnt.

```
Zähle i von 1 bis n-1
	einzusortierender_wert = A[ i ]
    j = i
    Solange j > 0 und A[ j-1 ] > einzusortierender_wert
	    A[ j ] = A[ j-1 ]
        j = j - 1
    A[ j ] = einzusortierender_wert
```

## Beispiel
Ausführung von Insertionsort auf Eingabefeld A [ 0..5 ]. Die Komponente, auf die der Index i zeigt, ist rot eingefärbt. Blau eingefärbte Felder liegen im bereits sortierten Teilfeld A [ 1.. i − 1 ].

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| 5 | 2 | 4 | 6 | 1 | 3 |

Da ein einzelnes Element keiner Ordnungsrelation unterliegt, beginnt der Index bei i = 1 und das zweite Element wird mit dem ersten verglichen.

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">5</font> | <font color="red">2</font> | 4 | 6 | 1 | 3 |

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">2</font> | <font color="red">5</font> | 4 | 6 | 1 | 3 |

Die 5 rutscht in der blauen sortierten Teilliste nach hinten und die 2 wird am Anfang dieser eingefügt. Damit sind die ersten beiden Elemente der Folge sortiert und das nächste Element wird überprüft ( i = 2 ).

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">2</font> | <font color="blue">5</font> | <font color="red">4</font>  | 6 | 1 | 3 |

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">2</font> | <font color="blue">4</font> | <font color="red">5</font>  | 6 | 1 | 3 |

Bei i = 3 ist nichts weiter zu tun, da 6 bereits die richtige Position am Ende der sortierten Teilliste hat.

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">2</font> | <font color="blue">4</font> | <font color="blue">5</font>  | <font color="red">6</font>  | 1 | 3 |

Im vorletzten Schritt wird die 1 ausgewählt und in die sortierte Liste eingefügt. Dabei rutschen alle bisherigen sortierten Elemente in der sortierten Liste um eins nach hinten ( i = 4 ).

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">2</font> | <font color="blue">4</font> | <font color="blue">5</font>  | <font color="blue">6</font>  | <font color="red">1</font>   | 3 |

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">1</font> | <font color="blue">2</font> | <font color="blue">4</font>  | <font color="blue">5</font>  | <font color="red">6</font>   | 3 |

Im letzten Schritt wird die 3 an passender Position in die sortierte Teilliste gebracht ( i = 5 ).

| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">1</font> | <font color="blue">2</font> | <font color="blue">4</font>  | <font color="blue">5</font>  | <font color="blue">6</font>   | <font color="red">3</font> |


| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| <font color="blue">1</font> | <font color="blue">2</font> | <font color="blue">3</font>  | <font color="blue">4</font>  | <font color="blue">5</font>   | <font color="red">6</font> |

Nach dem Algorithmus sind alle Felder der Folge sortiert.
| 0 | 1 | 2 | 3 | 4 | 5 |
| - | - | - | - | - | - |
| 1 | 2 | 3 | 4 | 5 | 6 |

## Komplexität

Die Anzahl der Vergleiche und Verschiebungen des Algorithmus ist von der Anordnung der Elemente in der unsortierten Eingangsfolge abhängig. Für den Average Case ist eine genaue Abschätzung der Laufzeit daher schwierig, man kann aber zeigen, dass der Average Case in O(n^2) liegt. Im Best Case, wenn das Eingabearray bereits sortiert ist, ist die Komplexität linear O(n), d. h. sogar besser als bei den komplizierteren Verfahren (Quicksort, Mergesort, Heapsort etc.). Im Worst Case ist sie quadratisch O(n^2).

Wenn zur Bestimmung der richtigen Position eines Elementes die binäre Suche benutzt wird, kann man die Anzahl der Vergleiche im Worst Case durch

    log(n!) ∈ O ( n log ⁡n − n log ⁡e + log ⁡n) = O(n log ⁡n − 0,4426n + log ⁡n )

abschätzen; dabei geht aber ggf. die Stabilität des Sortierverfahrens verloren.

Die Anzahl der Schiebeoperationen im Average Case beträgt

    n(n−1)/4 ∈ O(n^2).

Der Worst Case ist ein absteigend sortiertes Array A, da jedes Element von seiner Ursprungsposition j bis auf die erste Arrayposition verschoben wird und dabei j − 1 Verschiebeoperationen nötig sind. Deren Gesamtanzahl beträgt somit

    n(n−1)/2 ∈ O(n^2)

## Impelmentierung als Code

```C#
using System;

class Program
{
    static void Main()
    {
        int[] array = { 5, 2, 4, 6, 1, 3 };
        Console.WriteLine("Unsortiertes Array:");
        PrintArray(array);

        InsertionSort(array);

        Console.WriteLine("Sortiertes Array:");
        PrintArray(array);
    }

    static void InsertionSort(int[] array)
    {
        int n = array.Length;

        for (int i = 1; i < n; i++)
        {
            int einzusortierenderWert = array[i];
            int j = i - 1;

            // Verschiebe die Elemente, die größer als der einzusortierende Wert sind,
            // um eine Position nach hinten
            while (j >= 0 && array[j] > einzusortierenderWert)
            {
                array[j + 1] = array[j];
                j--;
            }
            // Füge den einzusortierenden Wert an der richtigen Position ein
            array[j + 1] = einzusortierenderWert;
        }
    }

    static void PrintArray(int[] array)
    {
        foreach (int value in array)
        {
            Console.Write(value + " ");
        }
        Console.WriteLine();
    }
}
```

## Links

* [Wikipedia](https://de.wikipedia.org/wiki/Insertionsort)
* [https://studyflix.de/informatik/insertionsort-1321](https://studyflix.de/informatik/insertionsort-1321)
