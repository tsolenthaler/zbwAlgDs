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