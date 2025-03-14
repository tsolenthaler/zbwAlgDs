# AVL-Tree Doppel Rotation
Ein AVL-Baum ist ein selbstbalancierender binärer Suchbaum, bei dem die Höhenbalance der Knoten beachtet wird. Bei jeder Einfügung oder Löschung wird sichergestellt, dass die Höhenunterschiede zwischen den linken und rechten Teilbäumen eines Knotens maximal 1 betragen. Wenn dieser Unterschied größer als 1 wird, sind Rotationen erforderlich, um den Baum wieder ins Gleichgewicht zu bringen.

Eine doppelte Rotation ist notwendig, wenn ein Knoten in den "äußeren" Teilbaum eines Knotens eingefügt wird, der bereits unbalanciert ist. Es gibt zwei Arten von doppelten Rotationen: Links-Rechts-Rotation und Rechts-Links-Rotation.

### Beispiel für einen AVL-Baum mit doppelter Rotation

#### Schritt 1: Einfügen von Knoten 30
```
    30
```

#### Schritt 2: Einfügen von Knoten 20
```
    30
   /
  20
```

#### Schritt 3: Einfügen von Knoten 10
```
    30
   /
  20
 /
10
```
Hier ist der Baum unbalanciert (Höhenunterschied = 2). Wir führen eine Rechtsrotation um Knoten 30 durch.

#### Nach der Rechtsrotation:
```
    20
   /  \
  10   30
```

#### Schritt 4: Einfügen von Knoten 25
```
    20
   /  \
  10   30
       /
      25
```

#### Schritt 5: Einfügen von Knoten 40
```
    20
   /  \
  10   30
       / \
      25  40
```

#### Schritt 6: Einfügen von Knoten 22
```
    20
   /  \
  10   30
       / \
      25  40
     /
    22
```
Jetzt ist der Baum unbalanciert (Höhenunterschied = 2) bei Knoten 30, und wir haben eine Links-Rechts-Situation (wir haben zuerst in den linken Teilbaum von 30 eingefügt). Daher führen wir eine doppelte Rotation durch: Zuerst eine Rechtsrotation um Knoten 25, gefolgt von einer Linksrotation um Knoten 30.

#### Rechtsrotation um Knoten 25:
```
    20
   /  \
  10   30
       / \
      22  40
     /
    25
```

#### Linksrotation um Knoten 30:
```
    20
   /  \
  10   22
       / \
      25  30
             \
              40
```

Jetzt ist der Baum wieder balanciert.

### Zusammenfassung der Schritte:
1. Einfügen von Knoten 30, 20, 10: Rechtsrotation um 30.
2. Einfügen von Knoten 25, 40: Baum bleibt balanciert.
3. Einfügen von Knoten 22: Doppelte Rotation (Rechts um 25, Links um 30).

Durch diese Schritte haben wir demonstriert, wie eine doppelte Rotation in einem AVL-Baum funktioniert, um die Balance nach einer Einfügung wiederherzustellen.