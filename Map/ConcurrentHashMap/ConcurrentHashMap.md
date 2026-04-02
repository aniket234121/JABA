# Concurrent HashMap
ConcurrentHashMap<K, V> is a thread-safe, high-performance implementation of the Map interface designed for concurrent access without full synchronization.

Introduced in Java 5 (java.util.concurrent)
Part of concurrent collections framework

## Key Characteristics
* Thread-safe without locking entire map
* Allows concurrent read and write operations
* No null keys or values allowed
* Higher performance than Hashtable in multithreaded environments
* Uses lock striping (Java 7) and CAS + synchronized bins (Java 8+)

## Internal Working
### Java 7 (Legacy Concept)

* Map divided into segments
* Each segment locked separately → improves concurrency


### Java 8+ (Modern Implementation)
Uses:
* CAS (Compare-And-Swap) for updates
* Synchronized blocks on bins (buckets)
Structure:
* Array of nodes (like HashMap)
* Buckets can become:
    * Linked List
    * Balanced Tree (Red-Black Tree) when threshold exceeded

```java
import java.util.concurrent.ConcurrentHashMap;

public class Main {
    public static void main(String[] args) {

        ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();

        // Adding elements
        map.put(1, "A");
        map.put(2, "B");
        map.put(3, "C");

        System.out.println("Map: " + map);

        // Atomic operation
        map.putIfAbsent(2, "X"); // won't replace
        map.putIfAbsent(4, "D");

        // Concurrent-safe update
        map.compute(3, (k, v) -> v + "-Updated");

        System.out.println("After updates: " + map);

        // Access
        System.out.println("Value for key 3: " + map.get(3));
    }
}
```
**Output:**

    Map: {1=A, 2=B, 3=C}
    After updates: {1=A, 2=B, 3=C-Updated, 4=D}
    Value for key 3: C-Updated

### **Concurrency Behavior**
| Operation               | Locking                 |
| ----------------------- | ----------------------- |
| Read (`get`)            | No lock (non-blocking)  |
| Write (`put`, `remove`) | Lock on specific bucket |
| Resize                  | Partial blocking        |
