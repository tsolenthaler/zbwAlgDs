---
tags:
  - MD02
  - Rekursion
---


## Eliminierung der Rekursion
Die Umwandlung eines rekursiven Algorithmus in eine iterative Form ist ein Prozess, der oft als
"Eliminierung der Rekursion" bezeichnet wird. Dies ist nicht immer geradlinig und hängt von der
Art der Rekursion ab. Es gibt zwei Hauptarten der Rekursion – lineare Rekursion und baumartige
(oder verzweigte) Rekursion.

Bei linearer Rekursion, wie beim rekursiven Berechnen der Fakultät oder der Fibonacci-Zahlen (in
der einfachen Form), kann man oft einfach einen iterativen Algorithmus formulieren, indem man
eine Schleife verwendet und den Zustand, der normalerweise durch rekursive Aufrufe verwaltet
wird, in lokalen Variablen speichert.

Für verzweigte oder baumartige Rekursion, bei der jeder rekursive Aufruf selbst mehrere
rekursive Aufrufe auslöst (wie bei vielen Baumdurchlaufalgorithmen oder beim rekursiven
Backtracking), ist der Prozess komplizierter. Hier sind einige allgemeine Schritte, die Sie für die
Umwandlung beachten sollten:

1. Stack verwenden: Da der Aufrufstapel bei der Rekursion implizit zum Speichern des
Zustands und zur Verwaltung der Aufrufe verwendet wird, muss man bei der Iteration
einen expliziten Stack benutzen. Manchmal muss auch eine Queue oder eine andere
Datenstruktur verwendet werden, je nachdem, in welcher Reihenfolge die Elemente
verarbeitet werden sollen.
2. Zustand erfassen: Bestimmen Sie den Zustand, der bei jedem rekursiven Aufruf
übertragen wird. Dies umfasst die Argumente der Funktion, lokale Variablen und jede
andere Information, die benötigt wird, um den rekursiven Aufruf nachzuahmen.
3. Endbedingung: Implementieren Sie die Endbedingung Ihrer Rekursion als
Abbruchbedingung in Ihrer Schleife.
4. Ersetzen von Aufrufen durch Iteration: Ersetzen Sie jeden rekursiven Aufruf durch das
Hinzufügen eines neuen Zustandsobjekts zum Stack.
5. Schleife konstruieren: Bauen Sie eine Schleife, die solange läuft, bis der Stack (oder eine
andere verwendete Datenstruktur) leer ist, und verarbeiten Sie jedes Element, indem Sie
den aktuellen Zustand so aktualisieren, wie es die Rekursion tun würde.

Beispiel siehe Lösung Aufgabe 2.3.3 im Buch «Algorithmen und Datenstrukturen in C#».