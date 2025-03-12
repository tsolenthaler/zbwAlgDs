# Fragen Binary Tree

## was ist im Speziellen ein Binary Search Tree?

Ein Binary Search Tree (BST) ist eine spezielle Art von Datenstruktur, die in der Informatik verwendet wird, um Daten effizient zu speichern und zu durchsuchen. Die Hauptmerkmale eines Binary Search Trees sind:

1. **Binäre Struktur**: Jeder Knoten in einem BST hat höchstens zwei Nachfolger, die als linkes und rechtes Kind bezeichnet werden.

2. **Ordnungseigenschaft**: Für jeden Knoten gilt:

   * Alle Werte im linken Teilbaum sind kleiner als der Wert des Knotens.
   * Alle Werte im rechten Teilbaum sind größer als der Wert des Knotens.

3. **Keine Duplikate**: In der Regel werden in einem BST keine doppelten Werte gespeichert, um die Integrität der Ordnung zu gewährleisten.

### Vorteile eines Binary Search Trees:
- **Effiziente Suche**: Die durchschnittliche Zeitkomplexität für die Suche, das Einfügen und das Löschen eines Knotens beträgt O(log n), wobei n die Anzahl der Knoten im Baum ist, vorausgesetzt, der Baum ist ausgewogen.
- **Einfache Implementierung**: Die Struktur ist relativ einfach zu implementieren und zu verstehen.

### Nachteile:
- **Ungleichgewicht**: Wenn der Baum nicht ausgewogen ist (z. B. wenn die Werte in aufsteigender oder absteigender Reihenfolge eingefügt werden), kann die Zeitkomplexität auf O(n) ansteigen, was die Effizienz verringert.
- **Speicherverbrauch**: Jeder Knoten benötigt zusätzlichen Speicher für die Zeiger auf die Kinder.

Um die Nachteile eines unbalancierten BSTs zu vermeiden, gibt es verschiedene selbstbalancierende Varianten, wie z. B. AVL-Bäume oder Rot-Schwarz-Bäume.