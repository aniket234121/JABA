# Array Deque

ArrayDeque is a resizable array-based implementation of the Deque interface, supporting double-ended operations (insert/remove from both front and rear).

It can act as:

* Queue (FIFO)
* Stack (LIFO)

## Key Characteristics
* **Resizable circular array**
* No capacity restriction (grows dynamically)
* **Faster than LinkedList (better cache locality)**
* Not thread-safe
* Null elements NOT allowed
* No index-based access (not a List)

## Core Operations
###  Queue Operations (FIFO)
    offer(e) → add at rear
    poll() → remove from front
    peek() → view front
###  Deque Operations (Both Ends)
    offerFirst(e)
    offerLast(e)
    pollFirst()
    pollLast()
    peekFirst()
    peekLast()
###  Stack Operations (LIFO)
    push(e)
    pop()
    peek()

## Internal Working
* Backed by Resizable Circular Array

        elements[] → internal array
        head → front index
        tail → next insertion index at rear

```java
import java.util.ArrayDeque;

public class Main {
    public static void main(String[] args) {
        ArrayDeque<Integer> dq = new ArrayDeque<>();

        // Queue behavior
        dq.offer(10);
        dq.offer(20);
        dq.offer(30);

        System.out.println(dq.poll()); // 10

        // Deque behavior
        dq.offerFirst(5);
        dq.offerLast(40);

        System.out.println(dq.peekFirst()); // 5
        System.out.println(dq.peekLast());  // 40

        // Stack behavior
        dq.push(100);
        System.out.println(dq.pop()); // 100
    }
}
```