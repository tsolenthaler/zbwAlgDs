# Implementierung Hashtable

## Hier ist ein einfaches Beispiel für eine Hashtable mit offener Adressierung in C#:
Eine Hashtable mit offener Adressierung in C# kann durch die Verwendung eines Arrays zur Speicherung der Schlüssel-Wert-Paare und einer geeigneten Hash-Funktion zur Berechnung des Index für die Speicherung und den Zugriff auf die Elemente implementiert werden. Offene Adressierung bedeutet, dass bei Kollisionen (d.h. wenn zwei Schlüssel denselben Hash-Wert erzeugen) nach dem nächsten verfügbaren Platz im Array gesucht wird.

Hier ist ein einfaches Beispiel für eine Hashtable mit offener Adressierung in C#:

```csharp
using System;

public class OpenAddressingHashtable<TKey, TValue>
{
    private const int InitialSize = 16;
    private (TKey Key, TValue Value)?[] _table;
    private int _count;

    public OpenAddressingHashtable()
    {
        _table = new (TKey, TValue)?[InitialSize];
        _count = 0;
    }

    private int GetHash(TKey key)
    {
        return Math.Abs(key.GetHashCode()) % _table.Length;
    }

    private int GetNextIndex(int index, int i)
    {
        return (index + i) % _table.Length;
    }

    public void Add(TKey key, TValue value)
    {
        if (_count >= _table.Length / 2)
        {
            Resize();
        }

        int index = GetHash(key);
        for (int i = 0; i < _table.Length; i++)
        {
            int probeIndex = GetNextIndex(index, i);
            if (_table[probeIndex] == null || _table[probeIndex].Value.Equals(default(TValue)))
            {
                _table[probeIndex] = (key, value);
                _count++;
                return;
            }
            else if (_table[probeIndex].Key.Equals(key))
            {
                _table[probeIndex] = (key, value); // Update existing value
                return;
            }
        }

        throw new InvalidOperationException("Hashtable is full");
    }

    public bool TryGetValue(TKey key, out TValue value)
    {
        int index = GetHash(key);
        for (int i = 0; i < _table.Length; i++)
        {
            int probeIndex = GetNextIndex(index, i);
            if (_table[probeIndex] == null)
            {
                value = default;
                return false; // Key not found
            }
            if (_table[probeIndex].Key.Equals(key))
            {
                value = _table[probeIndex].Value;
                return true; // Key found
            }
        }

        value = default;
        return false; // Key not found
    }

    private void Resize()
    {
        var oldTable = _table;
        _table = new (TKey, TValue)?[oldTable.Length * 2];
        _count = 0;

        foreach (var entry in oldTable)
        {
            if (entry.HasValue)
            {
                Add(entry.Value.Key, entry.Value.Value);
            }
        }
    }
}
```

### Erklärung des Codes:

1. **Datenstruktur**: Die Hashtable verwendet ein Array von Tupeln `(TKey, TValue)?`, um die Schlüssel-Wert-Paare zu speichern. Das Fragezeichen `?` bedeutet, dass die Elemente null sein können, was für leere Plätze in der Hashtable verwendet wird.

2. **Hash-Funktion**: Die Methode `GetHash` berechnet den Hash-Wert für einen gegebenen Schlüssel und stellt sicher, dass der Index im Bereich des Array-Längen bleibt.

3. **Kollisionsbehandlung**: Bei Kollisionen wird die Methode `GetNextIndex` verwendet, um den nächsten Index zu finden, indem eine lineare Sondierung durchgeführt wird.

4. **Hinzufügen von Elementen**: Die Methode `Add` fügt ein neues Schlüssel-Wert-Paar hinzu oder aktualisiert einen vorhandenen Wert, wenn der Schlüssel bereits existiert. Wenn die Hashtable zu mehr als der Hälfte gefüllt ist, wird sie vergrößert.

5. **Wert abrufen**: Die Methode `TryGetValue` versucht, einen Wert für einen gegebenen Schlüssel zu finden und gibt `true` zurück, wenn der Schlüssel gefunden wurde, andernfalls `false`.

6. **Resize**: Die Methode `Resize` verdoppelt die Größe der Hashtable und fügt alle vorhandenen Elemente in die neue Tabelle ein.

Diese Implementierung ist einfach und dient als Grundlage für eine Hashtable mit offener Adressierung. In einer produktiven Umgebung sollten zusätzliche Überlegungen wie die Behandlung von Löschoperationen und die Verwendung einer besseren Hash-Funktion angestellt werden.

## wie wird eine Hashtable mit verkettung / geschlossene Adressierung in C# implementiert?

Eine Hashtable mit Verkettung (auch als geschlossene Adressierung bekannt) kann in C# implementiert werden, indem für jeden Index im Array eine Liste (z.B. eine verkettete Liste oder eine `List<T>`) verwendet wird, um Kollisionen zu behandeln. Wenn mehrere Schlüssel denselben Hash-Wert erzeugen, werden sie in der Liste an diesem Index gespeichert.

Hier ist ein einfaches Beispiel für eine Hashtable mit Verkettung in C#:

```csharp
using System;
using System.Collections.Generic;

public class ChainedHashtable<TKey, TValue>
{
    private const int InitialSize = 16;
    private List<(TKey Key, TValue Value)>[] _table;
    private int _count;

    public ChainedHashtable()
    {
        _table = new List<(TKey, TValue)>[InitialSize];
        _count = 0;
    }

    private int GetHash(TKey key)
    {
        return Math.Abs(key.GetHashCode()) % _table.Length;
    }

    public void Add(TKey key, TValue value)
    {
        int index = GetHash(key);
        if (_table[index] == null)
        {
            _table[index] = new List<(TKey, TValue)>();
        }

        // Überprüfen, ob der Schlüssel bereits existiert und aktualisieren
        for (int i = 0; i < _table[index].Count; i++)
        {
            if (_table[index][i].Key.Equals(key))
            {
                _table[index][i] = (key, value); // Update existing value
                return;
            }
        }

        // Neuen Eintrag hinzufügen
        _table[index].Add((key, value));
        _count++;
    }

    public bool TryGetValue(TKey key, out TValue value)
    {
        int index = GetHash(key);
        if (_table[index] != null)
        {
            foreach (var entry in _table[index])
            {
                if (entry.Key.Equals(key))
                {
                    value = entry.Value;
                    return true; // Key found
                }
            }
        }

        value = default;
        return false; // Key not found
    }

    public bool Remove(TKey key)
    {
        int index = GetHash(key);
        if (_table[index] != null)
        {
            for (int i = 0; i < _table[index].Count; i++)
            {
                if (_table[index][i].Key.Equals(key))
                {
                    _table[index].RemoveAt(i);
                    _count--;
                    return true; // Key removed
                }
            }
        }

        return false; // Key not found
    }

    public int Count => _count;
}
```

### Erklärung des Codes:

1. **Datenstruktur**: Die Hashtable verwendet ein Array von Listen, um die Schlüssel-Wert-Paare zu speichern. Jede Liste enthält Tupel `(TKey, TValue)`, die die Schlüssel und Werte repräsentieren.

2. **Hash-Funktion**: Die Methode `GetHash` berechnet den Hash-Wert für einen gegebenen Schlüssel und stellt sicher, dass der Index im Bereich der Array-Länge bleibt.

3. **Hinzufügen von Elementen**: Die Methode `Add` fügt ein neues Schlüssel-Wert-Paar hinzu. Wenn der Schlüssel bereits existiert, wird der Wert aktualisiert. Wenn der Index im Array noch nicht initialisiert ist, wird eine neue Liste erstellt.

4. **Wert abrufen**: Die Methode `TryGetValue` sucht nach einem Wert für einen gegebenen Schlüssel. Wenn der Schlüssel gefunden wird, wird der Wert zurückgegeben.

5. **Entfernen von Elementen**: Die Methode `Remove` entfernt ein Schlüssel-Wert-Paar aus der Hashtable, wenn der Schlüssel vorhanden ist.

6. **Zähler**: Die Eigenschaft `Count` gibt die Anzahl der gespeicherten Elemente in der Hashtable zurück.

Diese Implementierung ist einfach und bietet eine grundlegende Funktionalität für eine Hashtable mit Verkettung. In einer produktiven Umgebung sollten zusätzliche Überlegungen wie die Handhabung von Kapazität und Lastfaktoren angestellt werden, um die Leistung zu optimieren.