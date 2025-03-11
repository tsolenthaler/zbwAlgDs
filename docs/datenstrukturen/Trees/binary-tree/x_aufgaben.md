# Implementierung

## Traversierung nach In-Order

Schreiben Sie eine Methode in C#, die die Traversierung eines binären Suchbaums in In-Order durchführt.

```C#
public class TreeNode
{
    public int Value;
    public TreeNode Left;
    public TreeNode Right;

    public TreeNode(int value)
    {
        Value = value;
        Left = null;
        Right = null;
    }
}
```

```C#
public class BinarySearchTree
{
    public TreeNode Root;

    public BinarySearchTree()
    {
        Root = null;
    }

    // Methode zur In-Order-Traversierung
    public void InOrderTraversal(TreeNode node)
    {
        if (node == null)
        {
            return;
        }

        // Zuerst den linken Teilbaum besuchen
        InOrderTraversal(node.Left);
        
        // Dann den aktuellen Knoten (Wurzel) besuchen
        Console.WriteLine(node.Value);
        
        // Schließlich den rechten Teilbaum besuchen
        InOrderTraversal(node.Right);
    }
}
```

```C#
class Program
{
    static void Main(string[] args)
    {
        BinarySearchTree bst = new BinarySearchTree();
        
        // Beispielknoten hinzufügen (hier sollten Sie eine Methode zum Hinzufügen von Knoten implementieren)
        bst.Root = new TreeNode(5);
        bst.Root.Left = new TreeNode(3);
        bst.Root.Right = new TreeNode(7);
        bst.Root.Left.Left = new TreeNode(2);
        bst.Root.Left.Right = new TreeNode(4);
        bst.Root.Right.Left = new TreeNode(6);
        bst.Root.Right.Right = new TreeNode(8);

        // In-Order-Traversierung durchführen
        Console.WriteLine("In-Order Traversal:");
        bst.InOrderTraversal(bst.Root);
    }
}
```