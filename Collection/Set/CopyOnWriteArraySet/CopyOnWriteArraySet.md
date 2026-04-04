# CopyOnWriteArraySet
A Set that uses an internal CopyOnWriteArrayList for all of its operations. Thus, it shares the same basic properties:
* It is best suited for applications in which set sizes generally stay small, read-only operations vastly outnumber mutative operations, and you need to prevent interference among threads during traversal.
* It is thread-safe.
* Mutative operations (add, set, remove, etc.) are expensive  since they usually entail copying the entire underlying array.
* Iterators do not support the mutative remove operation.
* Traversal via iterators is fast and cannot encounter interference from other threads. Iterators rely on unchanging snapshots of the array at the time the iterators were constructed.

## Internal Working
👉 Internally uses:

    CopyOnWriteArrayList<E>

### 📌 Copy-On-Write Mechanism

How it works:
* Read operations → Directly access array (no locking)
* Write operations → Create a new copy of array

```java
import java.util.concurrent.CopyOnWriteArraySet;

public class CopyOnWriteArraySetExample {
    public static void main(String[] args) {

        CopyOnWriteArraySet<String> set = new CopyOnWriteArraySet<>();

        set.add("A");
        set.add("B");
        set.add("C");
        set.add("A"); // duplicate ignored

        System.out.println("Set: " + set);

        // Safe iteration
        for (String s : set) {
            System.out.println(s);
        }

        set.remove("B");

        System.out.println("After removal: " + set);
    }
}
```
Output:

    Set: [A, B, C]
    A
    B
    C
    After removal: [A, C]

