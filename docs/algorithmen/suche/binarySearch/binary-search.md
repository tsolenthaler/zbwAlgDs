# Binary search


## Implementeriung

```C#
using System;

class Program
{
    static void Main()
    {
        int[] sortedArray = { 1, 3, 5, 7, 9, 11, 13, 15, 17, 19 };
        int target = 7;

        int index = BinarySearch(sortedArray, target);

        if (index != -1)
        {
            Console.WriteLine($"Element {target} gefunden an Index {index}.");
        }
        else
        {
            Console.WriteLine($"Element {target} nicht gefunden.");
        }
    }

    static int BinarySearch(int[] array, int target)
    {
        int left = 0;
        int right = array.Length - 1;

        while (left <= right)
        {
            int mid = left + (right - left) / 2;

            // Überprüfen, ob das Ziel das mittlere Element ist
            if (array[mid] == target)
            {
                return mid; // Ziel gefunden
            }

            // Wenn das Ziel größer ist, ignoriere die linke Hälfte
            if (array[mid] < target)
            {
                left = mid + 1;
            }
            // Wenn das Ziel kleiner ist, ignoriere die rechte Hälfte
            else
            {
                right = mid - 1;
            }
        }

        // Ziel nicht gefunden
        return -1;
    }
}
```

### Python
Python Code
```Python
def binäre_suche(folge: Sequence[int], x: int) -> Tuple[str, int]:
    links = 0
    rechts = len(folge) - 1

    while links <= rechts:
        mitte = links + (rechts - links) // 2  # Bereich halbieren
        if folge[mitte] == x: 
            return 'Position', mitte

        if folge[mitte] > x:
            rechts = mitte - 1  # im linken Abschnitt weitersuchen
        else:
            links = mitte + 1  # im rechten Abschnitt weitersuchen

    return 'Lücke', links
```