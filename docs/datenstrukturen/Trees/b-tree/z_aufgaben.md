# Aufgaben B-Tree

### Übungen

#### 1. Aufgabe

Zeichnen Sie den B-Tree 2. Ordnung welcher entsteht, wenn Elemente mit folgenden Schlüsseln
eingegeben werden:

```
25, 37, 42, 7, 18, 54, 1, 82, 17, 3, 21, 47, 51, 62, 73, 69, 8, 15, 91, 12, 24, 85
```

Es sollen alle Schritte sichtbar sein.

#### 2. Aufgabe

Fügen Sie im folgenden B-Tree zuerst das Element 42 ein. Löschen Sie anschliessend die Elemente 28 und 45. Zeichnen Sie nach jeder Operation den entsprechenden Baum.

#### 3. Aufgabe

Mit einem B-Tree sollen 10'000'000 Elemente so gespeichert werden, dass die Page, welches das Element beinhaltet, mit der Durchführung von max. 5 Schritten im B-Tree gefunden werden kann. Berechnen Sie die minimale Anzahl Keys 𝑑 pro Page.

### Wiederholungsaufgaben

#### 2. Aufgabe
In einem B-Tree sollen die Autokennzeichen des Kanton SG gespeichert werden. Da alle Kennzeichen im gleichen Kanton sind, muss das Kürzel nicht gespeichert werden. Um die Zahl des Kennzeichens zu speichern, wird eine 32Bit-Zahl verwendet. Ein Block auf der Disk ist 1024Byte gross. Mit einem Lesevorgang auf der Disk wird immer ein kompletter Block gelesen. 
In diesem B-Tree werden nun 500‘000 Kennzeichen gespeichert. Berechnen Sie die Anzahl Zugriffe auf die Disk, die maximal nötig sind, um ein gesuchtes Kennzeichen zu finden. Den Speicherbedarf für die Verlinkung der Nodes können Sie ignorieren. 

Antwort: 3 (falsch) --> 4

Wieso?

Um die Anzahl der Zugriffe auf die Disk zu berechnen, die maximal nötig sind, um ein gesuchtes Kennzeichen in einem B-Tree zu finden, müssen wir einige Schritte durchgehen.

1. **Blockgröße und Datenspeicherung**:
   - Ein Block hat eine Größe von 1024 Byte.
   - Jedes Kennzeichen wird als 32-Bit-Zahl gespeichert, was 4 Byte entspricht.
- Die Anzahl der Kennzeichen, die in einem Block gespeichert werden können, ist:
    ```math
    \text{Anzahl der Kennzeichen pro Block} = \frac{1024 \text{ Byte}}{4 \text{ Byte/Kennzeichen}} = 256 \text{ Kennzeichen}
    ```

2. **Anzahl der Kennzeichen**:
   - Es gibt insgesamt 500.000 Kennzeichen.

3. **Berechnung der Anzahl der Blöcke**:
   - Um die gesamte Anzahl der Kennzeichen zu speichern, benötigen wir:
   ```math
    \text{Anzahl der Blöcke} = \frac{500.000 \text{ Kennzeichen}}{256 \text{ Kennzeichen/Block}} \approx 1953,125
    ```

    Da wir keine Teilblöcke haben können, runden wir auf die nächste ganze Zahl auf:
    ```math
    \text{Anzahl der Blöcke} = 1954
    ```

4. **B-Tree Eigenschaften**:
   - Ein B-Tree hat eine bestimmte Ordnung \( t \), die die maximale Anzahl der Kinder pro Knoten bestimmt. Für die Berechnung nehmen wir an, dass der B-Tree optimal gefüllt ist.
   - In einem B-Tree mit Ordnung \( t \) kann jeder Knoten zwischen \( t-1 \) und \( 2t-1 \) Schlüssel haben und zwischen \( t \) und \( 2t \) Kinder.
   - Für eine grobe Schätzung nehmen wir an, dass jeder Knoten im B-Tree maximal \( 2t-1 \) Schlüssel hat. 

5. **Maximale Höhe des B-Trees**:
   - Wenn wir annehmen, dass jeder Knoten maximal 256 Kennzeichen (also 256 Schlüssel) speichern kann, dann ist die Anzahl der Kinder \( t \) in diesem Fall 256.
   - Die maximale Höhe \( h \) des B-Trees kann mit der Formel \( n \leq t^h \) abgeschätzt werden, wobei \( n \) die Anzahl der gespeicherten Elemente ist.
   - Um die Höhe zu finden, setzen wir \( n = 500.000 \) und \( t = 256 \):
     ```math
     256^h \geq 500.000
     ```
   - Um \( h \) zu finden, nehmen wir den Logarithmus zur Basis 256:
     ```math
     h \geq \log_{256}(500.000) = \frac{\log_{10}(500.000)}{\log_{10}(256)} \approx \frac{5.699}{2.408} \approx 2.37
     ```
   - Da die Höhe eine ganze Zahl sein muss, runden wir auf:
     ```math
     h = 3
     ```

6. **Maximale Zugriffe auf die Disk**:
   - Um ein gesuchtes Kennzeichen zu finden, müssen wir im schlimmsten Fall die Höhe des B-Trees an Diskzugriffen durchführen. Da wir in jedem Schritt einen Block lesen, benötigen wir maximal \( h + 1 \) Zugriffe (einen für den Wurzelknoten und einen für jeden weiteren Knoten auf dem Weg zum gesuchten Kennzeichen).
   - Daher ist die maximale Anzahl der Zugriffe auf die Disk:
     ```math
     \text{Maximale Zugriffe} = h + 1 = 3 + 1 = 4
     ```

Zusammenfassend benötigen Sie maximal **4 Zugriffe auf die Disk**, um ein gesuchtes Kennzeichen im B-Tree zu finden.