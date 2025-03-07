# Binary search Tree - Implementieren

## Implementieren
Implementieren Sie in C# eine Methode, die die Traversierung eines Binary Search Trees in Inorder durchführt.

```C#
using System;

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

public class BinarySearchTree
{
    public TreeNode Root;

    public BinarySearchTree()
    {
        Root = null;
    }

    // Methode zum Hinzufügen eines Wertes zum BST
    public void Insert(int value)
    {
        Root = InsertRec(Root, value);
    }

    private TreeNode InsertRec(TreeNode root, int value)
    {
        if (root == null)
        {
            return new TreeNode(value);
        }

        if (value < root.Value)
        {
            root.Left = InsertRec(root.Left, value);
        }
        else if (value > root.Value)
        {
            root.Right = InsertRec(root.Right, value);
        }

        return root;
    }

    // Inorder Traversierung
    public void InorderTraversal(TreeNode node)
    {
        if (node != null)
        {
            InorderTraversal(node.Left);   // Linker Teilbaum
            Console.Write(node.Value + " "); // Aktueller Knoten
            InorderTraversal(node.Right);  // Rechter Teilbaum
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        BinarySearchTree bst = new BinarySearchTree();
        bst.Insert(50);
        bst.Insert(30);
        bst.Insert(70);
        bst.Insert(20);
        bst.Insert(40);
        bst.Insert(60);
        bst.Insert(80);

        Console.WriteLine("Inorder Traversierung des BST:");
        bst.InorderTraversal(bst.Root);
    }
}
```