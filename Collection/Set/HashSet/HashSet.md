# HashSet
HashSet is a part of the Java Collections Framework and implements the Set interface. It represents a collection of unique elements (no duplicates allowed).

* Package: java.util
* Backed by: HashMap
* Allows: null (only one)
* Order: Unordered (no insertion order guarantee)

## Internal Working
* Internally uses a hash table (HashMap)
* Elements are stored as keys in HashMap
* A constant dummy object is used as value

```java
private transient HashMap<E,Object> map;
private static final Object PRESENT = new Object();
```
## Key Characteristics
| Feature            | Description                        |
| ------------------ | ---------------------------------- |
| Duplicate Elements | Not allowed                        |
| Null Values        | Only one allowed                   |
| Order              | Not maintained                     |
| Thread-safe        | ❌ No                               |
| Performance        | O(1) average for add/remove/search |


### Constructors
| Constructor                                      | Description                                                                          |
|--------------------------------------------------|--------------------------------------------------------------------------------------|
| `HashSet()`                                      | Creates an empty `HashSet` with default capacity (16) and load factor (0.75)         |
| `HashSet(int initialCapacity)`                   | Creates a `HashSet` with specified initial capacity                                  |
| `HashSet(int initialCapacity, float loadFactor)` | Creates a `HashSet` with specified capacity and load factor                          |
| `HashSet(Collection<? extends E> c)`             | Creates a `HashSet` containing elements of the given collection (removes duplicates) |


```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>();

        // Adding elements
        set.add("Apple");
        set.add("Banana");
        set.add("Mango");
        set.add("Apple"); // Duplicate

        System.out.println("Set: " + set);

        // Checking element
        System.out.println("Contains Mango? " + set.contains("Mango"));

        // Removing element
        set.remove("Banana");

        // Iterating
        for (String fruit : set) {
            System.out.println(fruit);
        }

        // Size
        System.out.println("Size: " + set.size());

        // Clear
        set.clear();
        System.out.println("Is Empty? " + set.isEmpty());
    }
}
```
#### Output:
    Set: [Apple, Mango, Banana]
    Contains Mango? true
    Apple
    Mango
    Size: 2
    Is Empty? true

