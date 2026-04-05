# Priority Queue
PriorityQueue is a queue implementation based on priority ordering, not FIFO.
Elements are ordered according to:

Natural ordering (Comparable) OR
Custom Comparator

By default, it behaves as a Min Heap.

* Not FIFO (priority-based removal)
* Heap-based implementation
* Duplicates allowed
* Null elements NOT allowed
* Not thread-safe
* **Default → Min Heap**

## Constructors (Important)
    PriorityQueue()
    PriorityQueue(int initialCapacity)
    PriorityQueue(Comparator<? super E> comparator)
    PriorityQueue(Collection<? extends E> c)

```java
import java.util.PriorityQueue;

public class Main {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        pq.offer(10);
        pq.offer(5);
        pq.offer(20);
        pq.offer(2);

        System.out.println(pq); // Not sorted output

        while (!pq.isEmpty()) {
            System.out.print(pq.poll() + " ");
        }
    }
}
```
## Output
    [2, 5, 20, 10]  // Internal heap representation (not sorted)
    2 5 10 20       // Correct priority order