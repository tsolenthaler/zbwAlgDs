# AVL-Tree Singel Rotation

Ein AVL-Baum ist ein selbstbalancierender binärer Suchbaum, bei dem die Höhenbalance der Knoten beachtet wird. Der Unterschied zwischen den Höhen der linken und rechten Teilbäume eines Knotens darf maximal 1 betragen. Wenn dieser Unterschied größer als 1 wird, muss der Baum durch Rotationen neu balanciert werden.

Hier ist ein detailliertes Beispiel für einen AVL-Baum mit einer einzelnen Rotation, um zu zeigen, wie die Balance wiederhergestellt wird.

### Schritt 1: Einfügen von Knoten

Nehmen wir an, wir fügen die folgenden Werte in der angegebenen Reihenfolge in den AVL-Baum ein: 30, 20, 10.

1. **Einfügen von 30**:
   ```
       30
   ```

2. **Einfügen von 20**:
   ```
       30
      /
     20
   ```

3. **Einfügen von 10**:
   ```
       30
      /
     20
    /
   10
   ```

### Schritt 2: Überprüfung der Balance

Nach dem Einfügen von 10 hat der Knoten 30 eine Höhe von 2 (links) und 0 (rechts), was einen Balancefaktor von 2 ergibt (Höhe links - Höhe rechts = 2 - 0 = 2). Dies ist nicht erlaubt, und wir müssen den Baum balancieren.

### Schritt 3: Durchführung einer Rotation

Da der Baum im linken Teilbaum von 30 (links-links-Fall) unausgeglichen ist, führen wir eine **Rechtsrotation** um den Knoten 30 durch.

#### Rechtsrotation um 30:

1. Der Knoten 20 wird der neue Wurzelknoten.
2. Der Knoten 30 wird zum rechten Kind von 20.
3. Der Knoten 10 bleibt das linke Kind von 20.

Nach der Rotation sieht der Baum so aus:

```
      20
     /  \
    10   30
```

### Schritt 4: Überprüfung der Balance nach der Rotation

Jetzt überprüfen wir die Balancefaktoren:

- Knoten 20: Höhe links (1) - Höhe rechts (1) = 0 (ausgeglichen)
- Knoten 10: Höhe links (0) - Höhe rechts (0) = 0 (ausgeglichen)
- Knoten 30: Höhe links (0) - Höhe rechts (0) = 0 (ausgeglichen)

Alle Knoten sind jetzt ausgeglichen, und der Baum ist ein gültiger AVL-Baum.

### Zusammenfassung

In diesem Beispiel haben wir einen AVL-Baum erstellt, der nach dem Einfügen von 30, 20 und 10 unausgeglichen wurde. Durch eine Rechtsrotation um den Knoten 30 haben wir den Baum erfolgreich balanciert. Dies ist ein typisches Beispiel für eine einzelne Rotation in einem AVL-Baum.