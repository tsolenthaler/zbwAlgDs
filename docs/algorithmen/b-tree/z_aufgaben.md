# Aufgaben

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

Antwort: 3

Wieso?