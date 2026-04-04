# Linked HashSet
LinkedHashSet is a class in the Java Collections Framework that:

* Implements Set
* Extends HashSet
* Maintains insertion order

**👉 It combines:**

* Hash table (for fast operations)
* Linked list (for order preservation)

**Constructors**

    LinkedHashSet()
    LinkedHashSet(int initialCapacity)
    LinkedHashSet(int initialCapacity, float loadFactor)
    LinkedHashSet(Collection<? extends E> c)

```java
import java.util.LinkedHashSet;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        LinkedHashSet<String> set = new LinkedHashSet<>();

        set.add("Apple");
        set.add("Banana");
        set.add("Mango");
        set.add("Apple"); // Duplicate

        System.out.println(set);

        set.remove("Banana");

        for (String fruit : set) {
            System.out.println(fruit);
        }
    }
}
```
Output:

    [Apple, Banana, Mango]
    Apple
    Mango