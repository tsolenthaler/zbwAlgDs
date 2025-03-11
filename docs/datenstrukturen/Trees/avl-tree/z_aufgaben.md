# Aufgaben

### Übungen

#### 1. Aufgabe
Entwickeln Sie den entstehenden AVLTree zeichnerisch. Alle durchzuführenden Rotationen sollen sichtbar sein. D.h. zeichnen Sie den Baum jeweils vor und nach der Rotation (inkl.Teilrotationen) auf.

```
70, 77, 65, 85, 83, 63, 61, 81, 82, 80, 73, 72, 75, 60
```

##### Start 1. Add 70

```
70
```
##### Add 77
```
70
  \
   77
```

##### Add 65
```
   70
  /  \
65   77
```

##### Add 85
```
   70
  /  \
65   77
       \
       85
```

##### Add 83
```
   70
  /  \
65   77
       \
       85
      /
     83
```

* Balancefaktor von 70 ist -2.
* Double Links-Rotation um 77
* RL(77)?
      * 1. LL(85)?
      * 2. RR(77)?
```
   70
  /  \
65   83
     / \
    77  85
```

##### Add 63
```
    70
   /  \
  65   83
 /     / \
63    77  85
```

##### Add 61
```
      70
     /  \
    65   83
   /     / \
  63    77  85
 /
61
```

* unausgeglichen / Balancefaktor von 65 ist 2
* LL(65)?
* Right Rotation um 63.
      * 63 Root und 61 left und 65 Right Child

```
        70
     /      \
    63      83
   /  \     / \
  61   65  77  85
```
##### Add 81

```
        70
     /      \
    63      83
   /  \     / \
  61   65  77  85
            \
            81
```

##### Add 82

```
        70
     /      \
    63      83
   /  \     / \
  61   65  77  85
            \
            81
              \
              82
```

* unbalanced --> left Rotation von 81.


```
        70
     /      \
    63      83
   /  \     / \
  61   65  81  85
           / \
          77  82
```

##### Add 80

```
        70
     /      \
    63      83
   /  \     / \
  61   65  81  85
           / \
          77  82
            \
            80
```

* unbalanced --> Right Rotation bei 81
      * 82 wird zum left Child von 83!

```
        70
     /       \
    63         81
   /  \      /    \
  61   65  77     83
            \     / \
            80   82  85
```

##### Add 73
```
        70
     /       \
    63          81
   /  \      /     \
  61   65   77      83
           / \      / \
          73  80   82  85
```
##### Add 72
```
        70
     /       \
    63          81
   /  \      /     \
  61   65   77      83
           / \      / \
          73  80   82  85
          /
         72
```

* unbalanced --> Double Left Rotation
* Steps ???
      * RL(70)
      * 1. LL(81)
      * 2. RR(70)

###### Steps

* 77 wird Root
* 73 wird zum right Child von 70, mit 72.
* 80 wird left Child von 81.

###### Abschluss

```
               77
          /        \
        70          81
     /     \        /  \
    63      73     80  83
   /  \     /          / \
  61   65  72        82   85
```
##### Add 75
```
               77
          /        \
        70          81
     /     \        /  \
    63      73     80  83
   /  \     / \        / \
  61   65  72  75    82   85
```
##### Add 60
```
               77
          /        \
        70          81
     /     \        /  \
    63      73     80  83
   /  \     / \        / \
  61   65  72  75    82   85
 /
60
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
