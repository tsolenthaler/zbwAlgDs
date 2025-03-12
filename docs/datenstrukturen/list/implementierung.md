# Implementierung List

## Singly Linked List (einfach verkettete Liste)

```C#
using System;

public class Node
{
    public int Data;
    public Node Next;

    public Node(int data)
    {
        Data = data;
        Next = null;
    }
}

public class SinglyLinkedList
{
    private Node head;

    public SinglyLinkedList()
    {
        head = null;
    }

    // Methode zum Hinzufügen eines Knotens am Ende der Liste
    public void Add(int data)
    {
        Node newNode = new Node(data);
        if (head == null)
        {
            head = newNode;
        }
        else
        {
            Node current = head;
            while (current.Next != null)
            {
                current = current.Next;
            }
            current.Next = newNode;
        }
    }

    // Methode zum Ausgeben der Liste
    public void PrintList()
    {
        Node current = head;
        while (current != null)
        {
            Console.Write(current.Data + " -> ");
            current = current.Next;
        }
        Console.WriteLine("null");
    }

    // Methode zum Entfernen eines Knotens mit einem bestimmten Wert
    public void Remove(int data)
    {
        if (head == null) return;

        if (head.Data == data)
        {
            head = head.Next;
            return;
        }

        Node current = head;
        while (current.Next != null)
        {
            if (current.Next.Data == data)
            {
                current.Next = current.Next.Next;
                return;
            }
            current = current.Next;
        }
    }

    // Methode zum Überprüfen, ob ein Wert in der Liste vorhanden ist
    public bool Contains(int data)
    {
        Node current = head;
        while (current != null)
        {
            if (current.Data == data)
            {
                return true;
            }
            current = current.Next;
        }
        return false;
    }
}

class Program
{
    static void Main(string[] args)
    {
        SinglyLinkedList list = new SinglyLinkedList();
        list.Add(1);
        list.Add(2);
        list.Add(3);
        list.PrintList(); // Ausgabe: 1 -> 2 -> 3 -> null

        list.Remove(2);
        list.PrintList(); // Ausgabe: 1 -> 3 -> null

        Console.WriteLine(list.Contains(3)); // Ausgabe: True
        Console.WriteLine(list.Contains(2)); // Ausgabe: False
    }
}
```

## Doubly Linked List (doppelt verkettete Liste)

```C#
using System;

public class Node
{
    public int Data;
    public Node Next;
    public Node Prev;

    public Node(int data)
    {
        Data = data;
        Next = null;
        Prev = null;
    }
}

public class DoublyLinkedList
{
    private Node head;

    public DoublyLinkedList()
    {
        head = null;
    }

    // Methode zum Hinzufügen eines Knotens am Ende der Liste
    public void AddLast(int data)
    {
        Node newNode = new Node(data);
        if (head == null)
        {
            head = newNode;
            return;
        }

        Node temp = head;
        while (temp.Next != null)
        {
            temp = temp.Next;
        }

        temp.Next = newNode;
        newNode.Prev = temp;
    }

    // Methode zum Entfernen eines Knotens
    public void Remove(Node nodeToRemove)
    {
        if (nodeToRemove == null) return;

        if (nodeToRemove.Prev != null)
        {
            nodeToRemove.Prev.Next = nodeToRemove.Next;
        }
        else
        {
            head = nodeToRemove.Next; // Wenn der zu entfernende Knoten der Kopf ist
        }

        if (nodeToRemove.Next != null)
        {
            nodeToRemove.Next.Prev = nodeToRemove.Prev;
        }
    }

    // Methode zum Durchlaufen der Liste
    public void PrintList()
    {
        Node temp = head;
        while (temp != null)
        {
            Console.Write(temp.Data + " ");
            temp = temp.Next;
        }
        Console.WriteLine();
    }
}

class Program
{
    static void Main(string[] args)
    {
        DoublyLinkedList list = new DoublyLinkedList();
        list.AddLast(1);
        list.AddLast(2);
        list.AddLast(3);
        list.PrintList(); // Ausgabe: 1 2 3

        // Entfernen eines Knotens
        Node nodeToRemove = list.head.Next; // Knoten mit Wert 2
        list.Remove(nodeToRemove);
        list.PrintList(); // Ausgabe: 1 3
    }
}
```