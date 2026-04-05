# PriorityBlockingQueue
An unbounded blocking queue that uses the same ordering rules as class PriorityQueue and supplies blocking retrieval operations.

While this queue is logically unbounded, attempted additions may fail due to resource exhaustion (causing OutOfMemoryError).

This class does not permit null elements. 

A priority queue relying on natural ordering also does not permit insertion of non-comparable objects (doing so results in ClassCastException).


    The queue is implemented as a binary heap
    Heap property ensures:
    The head element is always the smallest (or highest priority)
    BUT:
    Remaining elements are not globally sorted
    
## Internal Working (Critical Section)
Data Structure

Internally backed by a binary heap (array-based):

* Same concept as PriorityQueue
* Maintains heap invariant:
    * Min-heap (default) → smallest element at top
* Synchronization Model
    * Uses a single ReentrantLock
    * Not dual-lock like LinkedBlockingQueue
* Blocking Behavior (Important nuance ⚠️)
    * take() → blocks if queue is empty
    * put() → never blocks (because queue is unbounded)

### Constructors
| Constructor                 | Signature                                                                      | Ordering                      | Capacity Behavior                         | Internal Impact                                     | When to Use                                                 |
| --------------------------- | ------------------------------------------------------------------------------ | ----------------------------- | ----------------------------------------- | --------------------------------------------------- | ----------------------------------------------------------- |
| Default                     | `PriorityBlockingQueue()`                                                      | Natural (`Comparable`)        | Unbounded                                 | Creates heap with default size (11)                 | When elements already implement Comparable                  |
| Capacity                    | `PriorityBlockingQueue(int initialCapacity)`                                   | Natural                       | Unbounded (capacity is just initial size) | Reduces resizing overhead initially                 | When expecting large data, optimization needed              |
| Comparator (Most Important) | `PriorityBlockingQueue(int initialCapacity, Comparator<? super E> comparator)` | Custom ordering               | Unbounded                                 | Heap ordering controlled by comparator              | When priority logic is custom (real-world use)              |
| Collection आधारित           | `PriorityBlockingQueue(Collection<? extends E> c)`                             | Natural / existing comparator | Unbounded                                 | Uses **heapify (O(n))** instead of repeated inserts | Bulk initialization, faster than adding elements one by one |


### Scenario

A system processes tasks where higher priority tasks must execute first

```java
import java.util.concurrent.*;

class Task implements Comparable<Task> {
    int priority;
    String name;

    Task(int priority, String name) {
        this.priority = priority;
        this.name = name;
    }

    public int compareTo(Task other) {
        return other.priority - this.priority; // max-heap behavior
    }
}

public class Example {
    public static void main(String[] args) {
        PriorityBlockingQueue<Task> queue = new PriorityBlockingQueue<>();

        queue.put(new Task(1, "Low"));
        queue.put(new Task(5, "High"));
        queue.put(new Task(3, "Medium"));

        while (!queue.isEmpty()) {
            System.out.println(queue.take().name);
        }
    }
}
```
### Output:

    High
    Medium
    Low