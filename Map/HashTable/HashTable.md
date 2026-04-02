# HashTable

Hashtable<K, V> is a legacy synchronized class in Java that implements the Map interface and stores key-value pairs using a hash table data structure.

Hashtable is the oldest implementation of a hash table data structure in Java. The HashMap is the second implementation, which was introduced in JDK 1.2.

Both classes provide similar functionality, but there are also small differences,

## Key Characteristics
* Thread-safe (synchronized) by default
* Stores data as key-value pairs
* No null keys or null values allowed
* Keys are unique
* Values can be duplicated (but not null)
* Slower than HashMap due to synchronization overhead

```java
import java.util.Hashtable;

public class Main {
    public static void main(String[] args) {
        Hashtable<Integer, String> table = new Hashtable<>();

        // Adding elements
        table.put(1, "Apple");
        table.put(2, "Banana");
        table.put(3, "Cherry");

        System.out.println("Hashtable: " + table);

        // Accessing elements
        System.out.println("Value for key 2: " + table.get(2));

        // Checking presence
        System.out.println("Contains key 3: " + table.containsKey(3));

        // Removing element
        table.remove(1);

        System.out.println("After removal: " + table);
    }
}
```
**Output:**

    Hashtable: {3=Cherry, 2=Banana, 1=Apple}
    Value for key 2: Banana
    Contains key 3: true
    After removal: {3=Cherry, 2=Banana}