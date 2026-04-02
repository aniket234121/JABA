
# SortedMap (Interface)

SortedMap<K, V> is a subinterface of Map that maintains its entries sorted based on keys.

## Key Characteristics
Keys are stored in ascending order (natural ordering or via Comparator)

* Does not allow duplicate keys
* Provides range-view operations

### Important Methods
    firstKey() → returns the smallest key
    lastKey() → returns the largest key
    headMap(K toKey) → keys less than toKey
    tailMap(K fromKey) → keys greater than or equal to fromKey
    subMap(K fromKey, K toKey) → keys in range

Notes

Sorting is based on:
* Natural ordering (Comparable)
* Custom ordering (Comparator)

# NavigableMap (Interface)

NavigableMap<K, V> extends SortedMap and provides navigation methods for working with closest matches.

## Key Characteristics
* Supports bidirectional navigation
* Provides methods to find nearest keys
* Enables descending views

### Important Methods
    lowerKey(K key) → greatest key less than given key
    floorKey(K key) → greatest key ≤ given key
    ceilingKey(K key) → smallest key ≥ given key
    higherKey(K key) → smallest key greater than given key
    pollFirstEntry() → removes & returns first entry
    pollLastEntry() → removes & returns last entry
    descendingMap() → reverse order view

# TreeMap
TreeMap<K, V> is a Red-Black Tree-based implementation of NavigableMap

## Key Characteristics
Implements:
* Map
* SortedMap
* NavigableMap

Maintains sorted order of keys

Not synchronized

## Rules

Keys must be:

Comparable, or
Provided with a Comparator

Does NOT allow null keys

Allows multiple null values

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        // TreeMap implements NavigableMap
        NavigableMap<Integer, String> map = new TreeMap<>();

        map.put(10, "A");
        map.put(20, "B");
        map.put(30, "C");
        map.put(40, "D");

        System.out.println("Map: " + map);

        // SortedMap methods
        System.out.println("First Key: " + map.firstKey());
        System.out.println("Last Key: " + map.lastKey());

        // NavigableMap methods
        System.out.println("Lower than 25: " + map.lowerKey(25));
        System.out.println("Floor of 20: " + map.floorKey(20));
        System.out.println("Ceiling of 25: " + map.ceilingKey(25));
        System.out.println("Higher than 30: " + map.higherKey(30));

        // Range view
        System.out.println("SubMap (10 to 30): " + map.subMap(10, 30));

        // Descending order
        System.out.println("Descending Map: " + map.descendingMap());
    }
}
```
**Output:**

    Map: {10=A, 20=B, 30=C, 40=D}
    First Key: 10
    Last Key: 40
    Lower than 25: 20
    Floor of 20: 20
    Ceiling of 25: 30
    Higher than 30: 40
    SubMap (10 to 30): {10=A, 20=B}
    Descending Map: {40=D, 30=C, 20=B, 10=A}

* Use SortedMap → when only sorted keys are needed
* Use NavigableMap → when nearest-match navigation is required
*  Use TreeMap → when you need a concrete sorted + navigable implementation
