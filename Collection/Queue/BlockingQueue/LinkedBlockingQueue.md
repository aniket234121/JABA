# LinkedBlockingQueue
An optionally-bounded blocking queue based on linked nodes

The optional capacity bound constructor argument serves as a way to prevent excessive queue expansion. 

The capacity, **if unspecified, is equal to Integer.MAX_VALUE**. 

Linked nodes are dynamically created upon each insertion unless this would bring the queue above capacity.

**LinkedBlockingQueue is a thread-safe, optionally bounded FIFO queue backed by a linked node structure**

## Locks & Concurrency Model

This is the most important concept:

### 👉 It uses two separate locks:

putLock → for insertion
takeLock → for removal

### 👉 And two conditions:

* notFull → producers wait here
* notEmpty → consumers wait here
### Why 2 locks? (Critical optimization)

Unlike ArrayBlockingQueue (single lock), this allows:

One thread inserting while another is removing simultaneously
Reduces contention → higher throughput in multi-threaded systems
Flow of Operations

#### put(E e)

    Acquire putLock
    If queue is full → wait on notFull
    Add node at tail
    Increment count (atomic)
    Signal notEmpty
    Release lock

#### take()

    Acquire takeLock
    If queue is empty → wait on notEmpty
    Remove node from head
    Decrement count
    Signal notFull
    Release lock

👉 Count is maintained using AtomicInteger → avoids locking for size updates.

```java
import java.util.concurrent.*;

public class Example {
    public static void main(String[] args) {
        BlockingQueue<Integer> queue = new LinkedBlockingQueue<>(5);

        // Producer
        Runnable producer = () -> {
            try {
                for (int i = 1; i <= 10; i++) {
                    queue.put(i);
                    System.out.println("Produced: " + i);
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        };

        // Consumer
        Runnable consumer = () -> {
            try {
                while (true) {
                    Integer val = queue.take();
                    System.out.println("Consumed: " + val);
                }
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        };

        new Thread(producer).start();
        new Thread(consumer).start();
    }
}
```