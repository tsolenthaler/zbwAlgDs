# Heap Priorityqueue

## Ziele

- [ ] Ich kennen den Unterschied zwischen einem BinarySearchTree und einem Heap
- [ ] Ich kennen die grundlegenden Operationen eines Heaps
- [ ] Ich kennen mögliche Anwendungen eines Heaps


### Motivation

* Kontext: Planung von Flugrouten
    * Eine Fluggesellschaft muss täglich hunderte von Flügen planen und durchführen. Jeder Flug hat verschiedene Attribute, die seine Priorität beeinflussen können, wie z.B. die Flugzeit, die Anzahl der Passagiere, Wetterbedingungen und die strategische Bedeutung bestimmter Routen für das Netzwerk der Fluggesellschaft.
    * Es ist essentiell, dass die Fluggesellschaft in der Lage ist, ihre Ressourcen
    (Flugzeuge, Crews) effizient einzusetzen, um maximale Effizienz und Kundenzufriedenheit zu erreichen.

* Problemstellung: Effiziente Ressourcennutzung und Priorisierung
    * Das Kernproblem besteht darin, eine effiziente Reihenfolge für die Durchführung der Flüge zu finden, sodass:
    * Flüge mit höherer Priorität (z.B. Langstreckenflüge, Flüge mit vielen Passagieren, Flüge in Gebiete mit günstigen Wetterfenstern) vorrangig behandelt werden.
    * Ressourcen (Flugzeuge und Besatzungen) optimal genutzt werden, um Verspätungen zu minimieren und den Betrieb unter verschiedenen Umständen aufrechtzuerhalten.

* Häufig ist das Prinzip einer einfachen Warteschlange (Queue) nicht ausreichend
* Es sollen Elemente bevorzugt werden können
    * Planung von Flugrouten (Reihenfolge der Landung)
    * behinderte Personen
    * Prozessmanagement im Betriebssystem
    * Notfälle im Wartezimmer
* Lösung: die Elemente in einer Queue werden mit Prioritäten versehen
* Priorityqueue: Elemente werden in Abhängigkeit ihrer Priorität und ihrer Position aus der Warteschlange entnommen