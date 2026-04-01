# LinkedHashMap
The LinkedHashMap class is very similar to HashMap in most aspects. However, the linked hash map is based on both hash table and linked list to enhance the functionality of hash map.

**It maintains a doubly-linked list running through all its entries in addition to an underlying array of default size 16.**

To maintain the order of elements, the linked hashmap modifies the Map.Entry class of HashMap by adding pointers to the next and previous entries:

```java
static class Entry<K,V> extends HashMap.Node<K,V> {
    Entry<K,V> before, after;
    Entry(int hash, K key, V value, Node<K,V> next) {
        super(hash, key, value, next);
    }
}
```
Notice that the Entry class simply adds two pointers; before and after which enable it to hook itself to the linked list. Aside from that, it uses the Entry class implementation of a the HashMap.

## Key Features

| Feature          | Description                     |
| ---------------- | ------------------------------- |
| Order Maintained | Yes (Insertion or Access Order) |
| Null Keys        | 1 allowed                       |
| Null Values      | Multiple allowed                |
| Thread Safe      | ❌ No                            |
| Performance      | Slightly slower than `HashMap`  |
| Data Structure   | Hash table + Doubly Linked List |

## Constructors
```java
LinkedHashMap()
LinkedHashMap(int initialCapacity)
LinkedHashMap(int initialCapacity, float loadFactor)
LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder)
```
### Important:

accessOrder = false → Insertion Order (default)

accessOrder = true → Access Order (used in LRU cache)

---
### Insertion Order vs Access Order
**Insertion Order (default)**

    Put: A → B → C
    Iteration: A → B → C

**Access Order**

    Put: A → B → C
    Access B → Order becomes: A → C → B

#### Store student IDs and names while maintaining insertion order.
```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {
    public static void main(String[] args) {

        // Creating LinkedHashMap
        LinkedHashMap<Integer, String> students = new LinkedHashMap<>();

        // Adding entries
        students.put(101, "Aniket");
        students.put(102, "Rahul");
        students.put(103, "Sneha");

        // Accessing element
        System.out.println("Student with ID 102: " + students.get(102));

        // Iterating (Maintains insertion order)
        System.out.println("\nAll Students:");
        for (Map.Entry<Integer, String> entry : students.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```