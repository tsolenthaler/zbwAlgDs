# Aufgaben

### Übungen

#### 1. Aufgabe
Entwickeln Sie den entstehenden AVLTree zeichnerisch. Alle durchzuführenden Rotationen sollen sichtbar sein. D.h. zeichnen Sie den Baum jeweils vor und nach der Rotation (inkl.Teilrotationen) auf.

```
70, 77, 65, 85, 83, 63, 61, 81, 82, 80, 73, 72, 75, 60
```

#### 2. Aufgabe

Analog Aufgabe 1 jedoch mit folgenden Daten:
```
67, 6, 4, 80, 55, 40, 58, 48, 2, 50, 36, 49
```

#### 3. Aufgabe

In folgendem AVLTree sollen der Reihe nach, folgende Elemente gelöscht werden:
```
4, 8, 6, 5, 2, 1, 7, 3, 10
```
Zeichnen Sie den Baum nach jeder Löschoperation neu auf.

```
                 5
           /          \
          3             8
         / \         /     \
        2   4       7      10
       /           /       / \
      3           6       9  11
```


### Wiederholungsaufgaben

#### 1. Aufgabe

Gegeben ist der nachfolgende AVL-Tree: 

```
                 5
           /           \
          2            10
         / \         /    \
        1   4       8      12
           /       / \    / \
          3       7   9  11  13
                 /
                6
```

Nun wird der Knoten 3 gelöscht. Führen Sie die Balancierung mit Hilfe von Rotationen durch. Zeichnen Sie den Baum nach jeder einzelnen Rotation. Hinweis: Doppelte Rotationen (Left-Right- bzw. Right-Left-Rotation gelten als zwei Rotationen). 
