# TreeSet
TreeSet is a class in the Java Collections Framework that:

Implements NavigableSet (sub-interface of SortedSet)
Stores unique elements in sorted order
Uses a self-balancing binary search tree (Red-Black Tree) internally

## Internal Working
Core Concept

TreeSet internally uses:

    TreeMap<E, Object>

Elements are stored as keys
A dummy constant object is used as value

Internal Structure:

    private transient NavigableMap<E,Object> m;
    private static final Object PRESENT = new Object();



| Constructor                          | Description                                                                                    | Example                                                           |
|--------------------------------------|------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| `TreeSet()`                          | Creates an empty TreeSet sorted by natural order                                               | `TreeSet<Integer> set = new TreeSet<>();`                         |
| `TreeSet(Comparator<? super E> c)`   | Creates an empty TreeSet sorted using the specified comparator                                 | `TreeSet<String> set = new TreeSet<>(Comparator.reverseOrder());` |
| `TreeSet(Collection<? extends E> c)` | Creates a TreeSet containing the elements of the specified collection, sorted by natural order | `TreeSet<String> set = new TreeSet<>(List.of("a", "b", "a"));`    |
| `TreeSet(SortedSet<E> s)`            | Creates a TreeSet with the same elements and ordering as the given `SortedSet`                 | `TreeSet<Integer> set = new TreeSet<>(anotherSortedSet);`         |

```java
import java.util.TreeSet;

public class TreeSetDemo {
    public static void main(String[] args) {
        // Create TreeSet
        TreeSet<Integer> numbers = new TreeSet<>();

        // Adding elements
        numbers.add(50);
        numbers.add(10);
        numbers.add(30);
        numbers.add(20);
        numbers.add(10); // Duplicate (ignored)

        // Display TreeSet
        System.out.println("TreeSet: " + numbers);

        // Basic operations
        System.out.println("First element: " + numbers.first());
        System.out.println("Last element: " + numbers.last());
        System.out.println("Higher than 20: " + numbers.higher(20));
        System.out.println("Lower than 30: " + numbers.lower(30));
    }
}
```
#### Output:
    TreeSet: [10, 20, 30, 50]
    First element: 10
    Last element: 50
    Higher than 20: 30
    Lower than 30: 20

