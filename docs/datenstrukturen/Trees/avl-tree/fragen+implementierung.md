# Fragen und Implementierung AVL-Tree

## was ist der Unterschied zwischen einem unbalanced und balanced Tree
Der Unterschied zwischen einem unbalanced (unbalancierten) und einem balanced (balancierten) Tree liegt in der Struktur und der Effizienz der Datenorganisation.

1. **Unbalanced Tree (Unbalancierter Baum)**:
   - In einem unbalancierten Baum kann die Höhe des Baums im schlimmsten Fall linear sein, was bedeutet, dass der Baum wie eine verkettete Liste aussieht. Dies geschieht häufig, wenn die Daten in einer sortierten Reihenfolge eingefügt werden.
   - Die Such-, Einfüge- und Löschoperationen können in O(n) Zeit durchgeführt werden, wobei n die Anzahl der Knoten im Baum ist. Dies ist ineffizient, insbesondere bei großen Datenmengen.

2. **Balanced Tree (Balancierter Baum)**:
   - Ein balancierter Baum ist so strukturiert, dass die Höhe des Baums logarithmisch zur Anzahl der Knoten bleibt. Dies wird erreicht, indem der Baum bei Einfüge- und Löschoperationen regelmäßig neu balanciert wird.
   - Beispiele für balancierte Bäume sind AVL-Bäume und Rot-Schwarz-Bäume. In einem balancierten Baum sind die Such-, Einfüge- und Löschoperationen in O(log n) Zeit möglich, was eine deutlich bessere Leistung bietet.

Zusammenfassend lässt sich sagen, dass der Hauptunterschied in der Effizienz der Operationen und der Struktur des Baums liegt, wobei balancierte Bäume eine bessere Leistung bei der Verarbeitung von Daten bieten.

## Was ist ein AVLTree und wie geht seinen Balancing-Algorithmus?

Ein AVL-Baum (benannt nach den Erfindern Georgy Adelson-Velsky und Evgenii Landis) ist eine selbstbalancierende binäre Suchbaum-Datenstruktur. Der Hauptvorteil eines AVL-Baums besteht darin, dass er die Höhe des Baums im Vergleich zu einem normalen binären Suchbaum (BST) begrenzt, was zu einer garantierten logarithmischen Zeitkomplexität für Such-, Einfüge- und Löschoperationen führt.

### Eigenschaften eines AVL-Baums:
1. **Binärer Suchbaum**: Für jeden Knoten gilt, dass alle Werte im linken Teilbaum kleiner und alle Werte im rechten Teilbaum größer sind.
2. **Balanciert**: Für jeden Knoten im Baum ist der Höhenunterschied (Balancefaktor) zwischen dem linken und dem rechten Teilbaum höchstens 1. Der Balancefaktor wird definiert als:
   \[
   \text{Balancefaktor} = \text{Höhe des linken Teilbaums} - \text{Höhe des rechten Teilbaums}
   \]
   Ein Knoten ist:
   - **links balanciert** (Balancefaktor = +1)
   - **ausgeglichen** (Balancefaktor = 0)
   - **rechts balanciert** (Balancefaktor = -1)

### Balancing-Algorithmus:
Wenn ein Knoten in einen AVL-Baum eingefügt oder gelöscht wird, kann es notwendig sein, den Baum neu zu balancieren. Der Balancing-Algorithmus umfasst die folgenden Schritte:

1. **Einfügen**: Fügen Sie den neuen Knoten wie in einem normalen binären Suchbaum ein.
2. **Aktualisieren der Höhen**: Aktualisieren Sie die Höhen der Knoten, die auf dem Pfad von dem eingefügten Knoten bis zur Wurzel führen.
3. **Überprüfen des Balancefaktors**: Überprüfen Sie den Balancefaktor jedes Knotens auf dem Pfad zur Wurzel. Wenn der Balancefaktor eines Knotens 2 oder -2 beträgt, ist der Baum nicht mehr balanciert.
4. **Rotationen**: Führen Sie Rotationen durch, um den Baum wieder ins Gleichgewicht zu bringen. Es gibt vier Fälle:
   - **Links-Links (LL)**: Wenn ein Knoten in den linken Teilbaum des linken Kindes eingefügt wird, führen Sie eine Rechtsrotation durch.
   - **Rechts-Rechts (RR)**: Wenn ein Knoten in den rechten Teilbaum des rechten Kindes eingefügt wird, führen Sie eine Linksrotation durch.
   - **Links-Rechts (LR)**: Wenn ein Knoten in den rechten Teilbaum des linken Kindes eingefügt wird, führen Sie zuerst eine Linksrotation auf das linke Kind und dann eine Rechtsrotation auf den Knoten durch.
   - **Rechts-Links (RL)**: Wenn ein Knoten in den linken Teilbaum des rechten Kindes eingefügt wird, führen Sie zuerst eine Rechtsrotation auf das rechte Kind und dann eine Linksrotation auf den Knoten durch.

Durch diese Rotationen wird sichergestellt, dass der Baum nach jeder Einfüge- oder Löschoperation balanciert bleibt.

## wie wird ein AVLTree implementiert in C#?
Ein AVL-Baum ist ein selbstbalancierender binärer Suchbaum, bei dem die Höhenbalance der Knoten beibehalten wird. Hier ist eine einfache Implementierung eines AVL-Baums in C#:

```csharp
public class AVLTreeNode
{
    public int Key;
    public AVLTreeNode Left;
    public AVLTreeNode Right;
    public int Height;

    public AVLTreeNode(int key)
    {
        Key = key;
        Height = 1; // Höhe des neuen Knotens ist 1
    }
}

public class AVLTree
{
    private AVLTreeNode root;

    // Hilfsmethode zur Berechnung der Höhe eines Knotens
    private int GetHeight(AVLTreeNode node)
    {
        return node == null ? 0 : node.Height;
    }

    // Hilfsmethode zur Berechnung des Balancefaktors eines Knotens
    private int GetBalance(AVLTreeNode node)
    {
        return node == null ? 0 : GetHeight(node.Left) - GetHeight(node.Right);
    }

    // Rechtsrotation
    private AVLTreeNode RightRotate(AVLTreeNode y)
    {
        AVLTreeNode x = y.Left;
        AVLTreeNode T2 = x.Right;

        // Durchführung der Rotation
        x.Right = y;
        y.Left = T2;

        // Aktualisierung der Höhen
        y.Height = Math.Max(GetHeight(y.Left), GetHeight(y.Right)) + 1;
        x.Height = Math.Max(GetHeight(x.Left), GetHeight(x.Right)) + 1;

        // Rückgabe des neuen Wurzelknotens
        return x;
    }

    // Linksrotation
    private AVLTreeNode LeftRotate(AVLTreeNode x)
    {
        AVLTreeNode y = x.Right;
        AVLTreeNode T2 = y.Left;

        // Durchführung der Rotation
        y.Left = x;
        x.Right = T2;

        // Aktualisierung der Höhen
        x.Height = Math.Max(GetHeight(x.Left), GetHeight(x.Right)) + 1;
        y.Height = Math.Max(GetHeight(y.Left), GetHeight(y.Right)) + 1;

        // Rückgabe des neuen Wurzelknotens
        return y;
    }

    // Einfügen eines Schlüssels in den AVL-Baum
    public void Insert(int key)
    {
        root = Insert(root, key);
    }

    private AVLTreeNode Insert(AVLTreeNode node, int key)
    {
        // Normale BST-Einfügeoperation
        if (node == null)
            return new AVLTreeNode(key);

        if (key < node.Key)
            node.Left = Insert(node.Left, key);
        else if (key > node.Key)
            node.Right = Insert(node.Right, key);
        else
            return node; // Duplikate werden nicht erlaubt

        // Aktualisierung der Höhe des Vorfahrenknotens
        node.Height = 1 + Math.Max(GetHeight(node.Left), GetHeight(node.Right)));

        // Überprüfung des Balancefaktors und Durchführung der Rotationen
        int balance = GetBalance(node);

        // Links-Links-Fall
        if (balance > 1 && key < node.Left.Key)
            return RightRotate(node);

        // Rechts-Rechts-Fall
        if (balance < -1 && key > node.Right.Key)
            return LeftRotate(node);

        // Links-Rechts-Fall
        if (balance > 1 && key > node.Left.Key)
        {
            node.Left = LeftRotate(node.Left);
            return RightRotate(node);
        }

        // Rechts-Links-Fall
        if (balance < -1 && key < node.Right.Key)
        {
            node.Right = RightRotate(node.Right);
            return LeftRotate(node);
        }

        // Rückgabe des (unveränderten) Knotenszeigers
        return node;
    }

    // In-Order Traversierung des Baums
    public void InOrder()
    {
        InOrder(root);
    }

    private void InOrder(AVLTreeNode node)
    {
        if (node != null)
        {
            InOrder(node.Left);
            Console.Write(node.Key + " ");
            InOrder(node.Right);
        }
    }
}
```

### Verwendung des AVL-Baums

Hier ist ein Beispiel, wie man den AVL-Baum verwenden kann:

```csharp
class Program
{
    static void Main(string[] args)
    {
        AVLTree avlTree = new AVLTree();

        // Einfügen von Schlüsseln
        avlTree.Insert(10);
        avlTree.Insert(20);
        avlTree.Insert(30);
        avlTree.Insert(40);
        avlTree.Insert(50);
        avlTree.Insert(25);

        // In-Order Traversierung
        Console.WriteLine("In-Order Traversierung des AVL-Baums:");
        avlTree.InOrder(); // Ausgabe: 10 20 25 30 40 50
    }
}
```